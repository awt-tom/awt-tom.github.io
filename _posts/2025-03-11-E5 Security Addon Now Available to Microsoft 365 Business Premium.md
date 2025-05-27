---
title: E5 Security Addon Now Available to Microsoft 365 Business Premium
date: 2025-03-11
description: Enhance your Microsoft 365 Business Premium security with the E5 Security Addon. Gain access to advanced Defender features and security hardening tools.
categories: [Defender, Security, Microsoft 365]
tags: [  
  microsoft 365 business premium,
  e5 security addon,
  microsoft defender for endpoint plan 2,
  defender for identity,
  defender for office 365,
  defender for cloud apps,
  microsoft xdr,
  advanced hunting,
  safe links,
  phishing simulations,
  app registration monitoring,
  smb security,
  microsoft licensing,
  endpoint protection,
  microsoft security stack,
  security hardening,
  security add-on,
  defender for business
]
media_subpath: /assets/img/E5security
image:
  path: E5securitybanner.png
  width: 100%
  height: 100%
  alt: Enhance Microsoft 365 Business Premium with E5 Security Addon
---

### E5 Security Addon Now Available as Add-on to Microsoft 365 Business Premium

Since March 6, 2025, it is now possible to add the Microsoft E5 Security addon to your existing Microsoft 365 Business Premium license. This brings a whole new dimension to SMB security due to the inclusion of advanced security licenses and features in this addon.

### What Does E5 Security Add to Business Premium?

E5 Security enhances Microsoft 365 Business Premium with:

![Desktop View](E5overview.png)

- **Microsoft Entra ID Plan 2**
- **Microsoft Defender for Identity**
- **Microsoft Defender for Endpoint Plan 2**
- **Microsoft Defender for Office 365 Plan 2**
- **Microsoft Defender for Cloud Apps**

### Some benefits of the E5 Security Addon

- **30 days of advanced hunting** in Microsoft Defender, providing deeper insights into potential security threats. Your KQL geek will love you for adding this addon!
- **Six months of data retention** in the device timeline, allowing extended investigation periods.
- **Microsoft Defender XDR and Exposure Management**
- Your users will benefit from the **SafeLinks integration** into **M365 Copilot** which is to be rolled out end march and be completed end may.
- Create **phishing simulations** to raise awareness among your users (show your users how to detect and report phishing attempts).
- Monitor your **app registrations** and gain broader insights into their permissions and potential misconfigurations. 
- Surprisingly, it comes at a very **honest price**!

### Important Considerations

Microsoft has clarified:

> "If you choose this subscription setting, you won't be able to use your Defender for Business licenses. To better protect your organization, make sure you have enough Plan 2 licenses to cover every user."

### Understanding the Impact of This Change

What does this mean in practice?

When you use Microsoft 365 Business Premium, your users will have **Defender for Business** by default, as it is included in the Business Premium license. However, if you add the **E5 Security Add-on**, you must opt for full coverage with **Defender for Endpoint Plan 2**. This means that you will need to add the E5 Security add-on for every user in your environment, aligned with the number of Business Premium licenses assigned. Once you switch to **Defender for Endpoint Plan 2**, **Defender for Business will no longer be available**.

### Switch to Defender for Endpoint Plan 2

This transition does not happen automatically and requires manual action.

Go to [security.microsoft.com](https://security.microsoft.com){:target="_blank"}

Click on **Settings** > **Endpoints** > **License**

Here you will see the state of which license is in use. As you can see in the screenshot it is currently using "Defender for Business" by default. In order to make use of the **Defender for Endpoint Plan 2** we need to change this.

![Desktop View](Subscriptionstate.png)

Click "Manage subscription settings" to change this state. 

![Desktop View](Managesubsettings.png)

Here you will be able to choose "Microsoft Defender for Endpoint Plan 2"

Once selected and submitted you will be prompt to confirm.

![Desktop View](confirmchangestate.png)

> Caution: Read the prompt carefully!
{: .prompt-warning }

Once confirmed you will see that the current state has changed from "Microsoft Defender for Business" to "Microsoft defender for Endpoint Plant 2".

![Desktop View](statechanged.png)

> "Additionally, if you switch from **Microsoft Defender for Business** to **Microsoft Defender for Endpoint Plan 2**, it can take up to **six hours** for changes to reflect in the subscription state."


### Conclusion

The E5 Security add-on provides significant security enhancements for SMBs using Microsoft 365 Business Premium. Organizations should evaluate their licensing needs carefully to ensure seamless protection and compliance with Microsoft’s security recommendations. I believe this is a great start for SMB to get enterprise grade protection for a decent price. Ofcourse features do not come enabled by themselves so make sure to get out in the wild and learn more about all the new features that you can possibly add to your environment. Read my post about [Security coverage](https://azurewithtom.com/posts/Optimize-your-SOC-with-SIEM-and-XDR-Recommendations/){:target="_blank"} to see what you can add, such as Detection rules for Sentinel, enable product features for MDO and many more, or check out the security recommendations.

As always, thanks for reading! You can now leave a comment or if you have questions, drop them down below!
