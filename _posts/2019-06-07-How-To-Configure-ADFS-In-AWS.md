---
layout: post
status: publish
published: true
title: How To Configure ADFS In AWS
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2019-06-07 11:43:00 -0500'
date_gmt: '2019-06-07 11:43:00 -0500'
categories:
- Tutorial
tags: []
comments: []
---

Here are some quick references to configure ADFS in AWS. This is originally developed by Jeff on the [AWS Security Blog](https://aws.amazon.com/blogs/security/enabling-federation-to-aws-using-windows-active-directory-adfs-and-saml-2-0/)

1. Install ADFS Role and IIS role
2. Rename the server
3. Generate self-signed certificate
4. Configure ADFS role

Use the command below to download the ADFS metadata XML file

```
Invoke-WebRequest -Uri https://adfs.contoso.local/FederationMetadata/2007-06/FederationMetadata.xml -outfile FederationMetadata.xml
```

Configure ADFS with the neeed IAM ARNs for the SAML IDP and IAM Role:

- arn:aws:iam::AWS-ACCOUNT-ID:saml-provider/SAML
- arn:aws:iam::AWS-ACCOUNT-ID:role/SAML

Trusted Relying Party

```
https://signin.aws.amazon.com/static/saml-metadata.xml
```

Rule 1:
```
- Type: Transform an Incoming Claim
- Claim rule name: NameId
- Incoming claim type: Windows Account Name
- Outgoing claim type: Name ID
- Outgoing name ID format: Persistent Identifier
- Pass through all claim values: checked 
```

Rule 2:

```
- Rule Tye: Send LDAP Attributes as Claims
- Claim rule name: RoleSessionName 
- Attribute store: Active Directory 
- LDAP Attribute: E-Mail-Addresses 
- Outgoing Claim Type : https://aws.amazon.com/SAML/Attributes/RoleSessionName
```

Rule 3:

```
- Rule Type: Send Claims Using a Custom Rule
- Claim rule name: Get AD Groups
- Input the below:

c:[Type == "http://temp/variable", Value =~ "(?i)^AWS-"] => issue(Type = "https://aws.amazon.com/SAML/Attributes/Role", Value = RegExReplace(c.Value, "SAML", "arn:aws:iam::AWS-ACCOUNT-ID:saml-provider/SAML,arn:aws:iam::AWS-ACCOUNT-ID:role/SAML"));
```

Rule 4:

```
- Rule Type: Send Claims Using a Custom Rule
- Claim rule name: Roles
- Input the below to transpose the AD Group Name to IAM Role Name:

c:[Type == "http://temp/variable", Value =~ "(?i)^AWS-"] => issue(Type = "https://aws.amazon.com/SAML/Attributes/Role", Value = RegExReplace(c.Value, "AWS-", "arn:aws:iam::AWS-ACCOUNT-ID:saml-provider/ADFS,arn:aws:iam::AWS-ACCOUNT-ID:role/ADFS-"));

- Input the below to just pass the user

=> issue(Type = "https://aws.amazon.com/SAML/Attributes/Role", Value = "arn:aws:iam::AWS-ACCOUNT-ID:saml-provider/Apt922,arn:aws:iam::AWS-ACCOUNT-ID:role/SAML");
```

The below URL is the sign-in page:

```
https://localhost/adfs/ls/IdpInitiatedSignOn.aspx
```

For Windows 2016, you need to enable the page with the command below:

```
Set-AdfsProperties –EnableIdpInitiatedSignonPage $True
```