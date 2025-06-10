---
title: "Say Goodbye to Basic Authentication in Exchange Online: What You Need to Know"
date: 2025-05-20
description: "Prepare for the deprecation of Basic Authentication in Exchange Online by September 2025. Start detect legacy sign-ins (including ROPC) using Microsoft Entra ID, disabling Basic Auth in Microsoft 365, and migrating software to use more secure app registrations."
categories: [Microsoft Entra ID, Legacy Authentication]
tags: [
  exchange-online,
  basic-authentication,
  smtp-auth,
  microsoft-entra,
  sign-in-logs,
  oauth2,
  microsoft-graph-api,
  app-registration,
  scan-to-email,
  legacy-authentication
] # TAG names should always be lowercase
media_subpath: /assets/img/legacyauth
image:
  path: Basicauth.png
  width: 100%
  height: 100%
  alt:
---
## Say Goodbye to Basic Authentication in Exchange Online: What You Need to Know

Microsoft is making another move in its longterm mission to secure the modern workplace. As announced, **Basic Authentication for Client Submission (SMTP AUTH)** in Exchange Online will be **permanently disabled in September 2025**. And to be honest, it's about time! This change is to eliminate outdated and vulnerable authentication methods in favor of more secure, modern alternatives to send e-mail.

### What Is Basic Authentication and Why Is It Being Removed?

Client submission via authenticated SMTP is when a device or application sends outbound email using Microsoft 365, typically through smtp.office365.com:587.

Basic Authentication uses simple username and password credentials that are Base64 encoded. While this encoding provides minimal obfuscation, it's easily decoded. It later on transfers through TLS, which makes it encrypted. Yet it brings several security risks:

- **Phishing**: If intercepted, credentials can be easily gained
- **No multi-factor authentication support**: Basic Auth bypasses MFA entirely
- **Bruteforce**: Easier target for credential stuffing and brute force attacks

![Desktop View](basic-auth-sign.png)

Although most organizations have implemented the "Block Legacy Authentication" Conditional Access policy, many environments still have exceptions for printers, legacy applications, or other systems.

Modern authentication methods like OAuth use token-based authentication, significantly reducing these risks.

### Timeline and Communication

- **Mid-October 2024**: SMTP AUTH Client Submission Report will show whether Basic Auth or OAuth is being used.
- **January 2025**: Tenants using Basic Auth will receive a Message Center post.
- **August 2025**: Final reminder Message Center post.
- **September 2025**: Basic Auth permanently disabled. Affected clients will receive:
  > 550 5.7.30 Basic authentication is not supported for Client Submission.

## How to Identify Basic Authentication Usage

### Using Microsoft Entra Sign-In Logs

You can track Basic Auth usage using **Microsoft Entra Sign-In Logs**:

- Navigate to **Microsoft Entra > Identity > Users > Sign-in logs**
- Apply these filters:
   - **Client App**: Select *Authenticated SMTP*, *Exchange ActiveSync*, *IMAP*, *POP*, *Other clients*
   - **Status**: Filter on *Success* to see active usage (failures often indicate blocked attempts)

![Desktop View](Client-app-list.png)

Focus on successful sign-ins to identify which users, devices, or applications are actively using Basic Authentication. You'll commonly find:
- Multifunction printers (MFPs) using scan-to-email
- Legacy business applications
- Custom scripts or tools
- Older mobile devices

> **Important Note**: If you're using third-party software or line-of-business applications that send email using your domain, those will need to switch to modern authentication. This often involves configuring an **App Registration in Microsoft Entra ID** and granting the application appropriate permissions to send mail on behalf of a user or mailbox.
{: .prompt-tip }

### The kusto way

Use **Kusto Query Language (KQL)** in Log Analytics for more advanced analysis if logs are being sent to a Log Analytics workspace.

An example query:
```
SigninLogs
| where TimeGenerated > ago(5d)
| where not(ClientAppUsed has "Mobile Apps and Desktop clients")
| where not(ClientAppUsed has "Browser")
| where ClientAppUsed == "Authenticated SMTP"
| summarize arg_max(TimeGenerated,*) by UserPrincipalName
```
This query looks for users who signed in using only the legacy protocol “Authenticated SMTP” in the past 5 days.
It excludes any sign-ins using modern clients or browsers, helping to identify accounts still relying on outdated authentication methods.

## Migration options

### Multifunction Printers

Most modern printers support OAuth authentication:

- **Check printer firmware**: Ensure you're running the latest version (Who knows if new features have been added)
- **Contact your vendor**: Ask about OAuth/modern authentication support (They should have by now!)
- **Configure app registration**: Create a dedicated app registration for printer authentication
- **Test thoroughly**: Verify scan-to-email functionality before the deadline (september)

### Applications

Applications sending email programmatically should move to:

- **Microsoft Graph API**: The modern alternative for sending emails
- **OAuth 2.0 with client credentials flow**: For service-to-service authentication
- **Application permissions**: Grant appropriate Mail.Send permissions

In most cases it is vendor specific how the app registration is being configured. Always make sure that you checkout the permission requirements and think about what this means. Nowadays there are many types of permissions. So the day of "Permission to all" is long gone!

### Checklist

So lets grab a little checklist which we can use to go towards our endgoal, september, the month where we say goodbye to basic authentication.

- Audit current Basic Auth usage using sign-in logs
- Identify all devices, applications, and services using SMTP AUTH
- Contact vendors for modern authentication support
- Create app registrations for each service requiring email sending (See vendor knowledge items which permissions)
- Configure OAuth authentication in applications
- Test email functionality in the app/printers
- Update monitoring and alerting for new authentication methods
- Schedule migration completion before September 2025

## Lets remove the basic-authentication door

So lets remove the entire door and its frame and brick it up so no one can knock on it ever again.

- **Navigate to Microsoft 365 Admin Center**
- **Go to Settings > Org Settings**
- **Search for "Modern authentication"**
- **Disable "Authenticated SMTP"**

> **Warning**: Only disable after confirming no critical services depend on Basic Auth. Use the sign-in logs to verify no recent successful authentications.
{: .prompt-warning }

## Conclusion

The deprecation of Basic Authentication in Exchange Online represents a significant security improvement for Microsoft 365 environments. While the migration requires planning and effort, it will be worth it as it keeps your sign-in logs more clean, increase your security posture and will have better opportunities to monitor.


