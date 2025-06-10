---
title: The hidden danger of device code phishing
date: 2025-02-18
description: Currently there is a peak in abuse of device codes which are gathered by phishing attempts
categories: [Microsoft Entra ID, Conditional Access]
tags: [  
  device code phishing,
  microsoft defender,
  entra id,
  conditional access,
  phishing detection,
  storm-2372,
  device registration abuse,
  azure ad sign-in logs,
  device code flow,
  teams phone security,
  authentication flow abuse,
  azure security,
  microsoft 365 security,
  token-based attacks,
  refresh token abuse,
  rogue device registration,
  attacker persistence,
  kql phishing detection
] # TAG names should always be lowercase
media_subpath: /assets/img/devicecode
image:
  path: devicecode.png
  width: 100%
  height: 100%
  alt:
---
# So whats up with the DeviceCodes?

Microsoft recently revealed an ongoing phishing campaign by Storm-2372, targeting authentication methods that use device codes. This attack demonstrates a growing trend in phishing tactics, where attackers exploit weaknesses in authentication flows that are meant to improve user experience on devices with limited input capabilities.

## How Device Code Phishing Works

Device codes are typically used for signing into devices with limited options, such as smart TVs, IoT devices, and even tools like Microsoft Teams Phones. Instead of entering credentials directly on the device, the user is prompted to enter a code on a separate browser session to authenticate. This process is convenient but presents security risks, particularly in phishing scenarios. Why? Look at this.


![Desktop View](Devicecodeattackcycle.png)
**Figure 1:** Device code phishing attack flow

Storm-2372 abuses this authentication flow by tricking users into entering malicious device codes on legitimate Microsoft authentication portals. Once the attacker generated code is entered, they receive valid authentication tokens, effectively bypassing traditional security features like Multi-Factor Authentication (MFA). This method allows attackers to gain persistent access to accounts without directly stealing passwords.

Additionally, attackers no longer need to steal passwords to compromise accounts. By leveraging this technique, they eliminate an entire attack phase, streamlining their access to sensitive data.

### Storm-2372's Advanced Techniques: Exploiting Client IDs and Refresh Tokens

Another alarming trend observed in the last few days is Storm-2372’s use of the Microsoft Authentication Broker client ID to obtain a refresh token.

### Storm-2372 Attack Steps Explained

- **Identify Target & Initiate Device Code Flow Exploitation**

  - The attacker initiates the device code authentication flow using the Microsoft Authentication Broker client ID.
  - This enables them to receive a refresh token upon successful authentication.

- **Obtain Refresh Token for Device Registration Service**

  - With the obtained refresh token, the attacker can request another authentication token specifically for the device registration service in Microsoft Entra ID.
  - This step is crucial as it allows them to register an attacker controlled device in the organization's Entra ID. Oops!

- **Register Attacker Controlled Device**

  - The attacker registers a rogue device using the acquired token.
  - The device is now trusted by the organization’s Entra ID.

- **Obtain a Primary Refresh Token (PRT)**

  - With the rogue device registered, the attacker requests a Primary Refresh Token (PRT), which provides persistent access to the organization’s resources.

- **Access Organizational Resources**

  - Using the PRT, the attacker gains access to internal corporate applications, email services (e.g., Exchange Online), and possibly sensitive data.
  - The attacker can now exfiltrate emails or other valuable information.

- **Use Regional Proxies to Evade Detection**

  - The attacker routes traffic through geographically appropriate proxies matching the target organization’s region.
  - This helps bypass location based security alerts and reduces suspicion on anomalys.

- **Persistence & Further Exploitation**

  - The attacker maintains access via the rogue device and refreshes tokens to avoid reauthentication.
  - They may use stolen data for further attacks, phishing, or lateral movement within the organization.
  - Exfiltrating data

## The Risk for Organizations

Device code authentication was designed for ease of use, but its inherent design flaw is that it does not inherently verify *who* is entering the code that a valid code has been provided. This makes it a target for phishing campaigns. Organizations that allow device code authentication without proper restrictions expose themselves to risks.

Therefore it is worth the hassle to take some precaution to prevent abuse in the future. But there are some considerations to be made.

## Challenges with Teams Phones and Device Code Restrictions

While restricting or outright disabling device code authentication is an effective security measure, it can cause operational issues for devices that rely on this flow. Such as Microsoft Teams Phones. These phones often require device code authentication because they lack the capability to input full credentials.

Organizations looking to enforce stronger security while maintaining functionality should consider:

- **Restricting Device Code Flow** – Blocking device code authentication for all but necessary devices.
- **Creating Conditional Access Exclusions** – Allowing only pre-approved devices, such as Teams Phones, to use device code authentication.
- **Monitoring and Auditing Device Logins** – Ensuring that device code logins are only coming from expected locations and devices.
- **Educating Users on Phishing Risks** – Making sure your employees understand that attackers may try to trick them into entering device codes. Show them examples upfront so that there is a visual aspect.

Example of a Conditional access policy you can use.

This Conditional Access policy is designed to **block all device code authentication** in an organization. You can either import this one or click one together yourself.

Here's how it works in simple terms:

- It applies to **all users** and **all applications**.
- It specifically targets **device code authentication** (used for logging into devices with limited input capability as stated above).
- The policy states that if a user tries to sign in using the **device code flow**, the request will be **blocked**.
- The **state is "disabled"**, change this to **Report-Only** or **Enabled** once all is set.
- If enabled, this would **prevent attackers from abusing device code phishing techniques** but may also impact devices like **Teams Phones** that rely on this method.
- Make sure to test and exclude where needed. Create a trusted device group in case there are **Teams Phone** devices which can be excluded from the policy. 

```json
  {
    "displayName": "CA403-All-Block-DeviceCode-All-All-Block",
    "createdDateTime": null,
    "modifiedDateTime": null,
    "state": "disabled",
    "partialEnablementStrategy": null,
    "sessionControls": null,
    "conditions": {
      "userRiskLevels": [],
      "signInRiskLevels": [],
      "clientAppTypes": [
        "all"
      ],
      "platforms": null,
      "locations": null,
      "times": null,
      "deviceStates": null,
      "devices": null,
      "clientApplications": null,
      "applications": {
        "includeApplications": [
          "All"
        ],
        "excludeApplications": [],
        "includeUserActions": [],
        "includeAuthenticationContextClassReferences": [],
        "applicationFilter": null
      },
      "users": {
        "includeUsers": [
          "All"
        ],
        "excludeUsers": [],
        "includeGroups": [],
        "excludeGroups": [],
        "includeRoles": [],
        "excludeRoles": [],
        "includeGuestsOrExternalUsers": null,
        "excludeGuestsOrExternalUsers": null
      },
      "authenticationFlows": {
        "transferMethods": "deviceCodeFlow"
      }
    },
    "grantControls": {
      "operator": "OR",
      "builtInControls": [
        "block"
      ],
      "customAuthenticationFactors": [],
      "termsOfUse": [],
      "authenticationStrength": null
    }
  }
```

## Detections in XDR

Microsoft has published a KQL query which can be used to identity possible device code phishing attempts. If your organisation is not using devices codes allot there is the option to just go to the Entra ID portal and see the sign-in logs for yourself and filter for the Device Code sign-ins. 


**What does it search for?**

This query identifies users who clicked phishing links that contained "microsoft.com/devicelogin", "login.microsoftonline.com/common/oauth2/deviceauth", then logged in. It then looks at Entra ID sign-ins where the same users had a successful login as in (ErrorCode == 0). There is also A check on time as this is the time where the code is being added as input. You might want to play with this time as it can take up longer between the click and possible login.

```
let suspiciousUserClicks = materialize(UrlClickEvents
    | where ActionType in ("ClickAllowed", "UrlScanInProgress", "UrlErrorPage") or IsClickedThrough != "0"
    | where UrlChain has_any ("microsoft.com/devicelogin", "login.microsoftonline.com/common/oauth2/deviceauth")
    | extend AccountUpn = tolower(AccountUpn)
    | project ClickTime = Timestamp, ActionType, UrlChain, NetworkMessageId, Url, AccountUpn);
//Check for Risky Sign-In in the short time window
let interestedUsersUpn = suspiciousUserClicks
    | where isnotempty(AccountUpn)
    | distinct AccountUpn;
let suspiciousSignIns = materialize(AADSignInEventsBeta
    | where ErrorCode == 0
    | where AccountUpn in~ (interestedUsersUpn)
    | where RiskLevelDuringSignIn in (10, 50, 100)
    | extend AccountUpn = tolower(AccountUpn)
    | join kind=inner suspiciousUserClicks on AccountUpn
    | where (Timestamp - ClickTime) between (-2min .. 7min)
    | project Timestamp, ReportId, ClickTime, AccountUpn, RiskLevelDuringSignIn, SessionId, IPAddress, Url
);
//Validate errorCode 50199 followed by success in 5 minute time interval for the interested user, which suggests a pause to input the code from the phishing email
let interestedSessionUsers = suspiciousSignIns
    | where isnotempty(AccountUpn)
    | distinct AccountUpn;
let shortIntervalSignInAttemptUsers = materialize(AADSignInEventsBeta
    | where AccountUpn in~ (interestedSessionUsers)
    | where ErrorCode in (0, 50199)
    | summarize ErrorCodes = make_set(ErrorCode) by AccountUpn, CorrelationId, SessionId
    | where ErrorCodes has_all (0, 50199)
    | distinct AccountUpn);
suspiciousSignIns
| where AccountUpn in (shortIntervalSignInAttemptUsers)
```

## Final Thoughts

Device code authentication is useful, but it comes with significant risks. The Storm-2372 campaign highlights the need for organizations to carefully evaluate their use of device codes and apply security controls where necessary. While disabling it entirely may not be an option for every organization, especially those relying on Teams Phones. By creating well defined exceptions and security policies this can minimize risk without breaking any functionality.

For organizations using Microsoft cloud services, now is the time to review Conditional Access policies and strengthen authentication controls before attackers take advantage of this growing threat vector.

As always, stay safe!
