---
title: Whats New in Windows Autopatch
date: 2025-05-20
description: "Learn how Windows Autopatch lets you orchestrate updates for Windows, Microsoft 365 Apps, Microsoft Edge, and Teams. All from a single automated solution. Discover what's new in 2025, including hotpatching, improved reporting, and least-privilege access."
categories: [Windows Autopatch, Microsoft Intune, Patch Management]
tags: [
  windows autopatch,
  microsoft autopatch,
  autopatch licensing,
  autopatch hotpatch,
  windows 11 hotpatching,
  microsoft intune autopatch,
  intune patch management,
  m365 updates,
  windows 11 updates,
  feature updates,
  security updates,
  windows update rings
] # TAG names should always be lowercase
media_subpath: /assets/img/Windows_Autopatch
image:
  path: autopatch.png
  width: 100%
  height: 100%
  alt:
---
## What is Windows Autopatch?

Windows Autopatch is a cloud service that helps you automate Windows, Microsoft 365 Apps, Microsoft Edge and Microsoft Teams updates to reduce the exposure of your devices.

Rather than maintaining complex infrastructure, many businesses simply want their devices to stay secure and their users to stay productive, without IT teams struggling to update their devices. Windows Autopatch is designed with that goal in mind.

Here’s how it helps:

- **Keep Windows secure and up-to-date**: By automatically deploying monthly updates, Autopatch helps close the security gap and keeps endpoints protected with the latest patches.
- **Empower your users**: Updates for Microsoft 365 Apps, Microsoft Edge, and Teams roll out with new features and performance improvements. This gives users the latest tools to collaborate and work more efficiently.
- **Make IT more easy**: Routine update deployment is automated, allowing IT teams to focus on strategic work rather than day-to-day patching tasks.
- **Easy onboarding**: Enrolling in Windows Autopatch is quick and straightforward. It’s built into Microsoft Intune and minimizes the time and effort required from IT Admins.
- **Low user disruption**: Updates are rolled out in deployment rings, which use real-time feedback signals to reduce the likelihood of disruptions or compatibility issues.

Windows Autopatch reduces the manual effort and planning traditionally required for updating Windows, Microsoft 365 Apps, Microsoft Edge, and Teams.

---

## Licenses and features

### Licenses

In March 2025, Microsoft announced that Windows Autopatch is now also available for the Business Premium licenses, making it more accessible for small and medium-sized businesses. Together with the ability to add a Microsoft 365 E5 Security addon to Microsoft Business Premium license that is great news for SMB!

Windows Autopatch currently is available to the following licenses:

- Microsoft 365 Business Premium
- Windows 10/11 Education A3 or A5 (included in Microsoft 365 A3 or A5)
- Windows 10/11 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
- Windows 10/11 Enterprise E3 or E5 VDA

### Features

- **Update rings**  
  Manage update rings for Windows 10 and later devices directly through Windows Autopatch.  

- **Autopatch groups**  
  Use Autopatch groups to organize update deployments based on a set of devices. Each group is a logical container that combines Microsoft Entra groups with update policies like Update Rings and Feature Updates. 

- **Windows quality updates**  
  Manage quality update profiles for Windows 10 and later. You can expedite updates using targeted policies. Microsoft claims that Autopatch aims to keep 95% of devices on the latest quality update.

- **Hotpatch updates**  
  Install Monthly “B” release security updates without requiring a reboot.
  
> **Note:** On may 7th Microsoft announced that Hotpatch is now available for Devices running Windows 11. The documentation still states that Windows 11 Enterprise is still required. Microsoft 365 Business Premium includes only Windows 11 Pro by default, which does not support hotpatching if we may believe the current documentation.  
> 
> **Let's hope Microsoft will add/change this for our SMB friends asap!**
{: .prompt-tip }

- **Windows feature updates & multi-phase release policies**  
  Customize and stage annual Windows feature updates across multiple deployment phases. Tailor them to specific Autopatch groups for better control. This is great if you want specific departments to roll out new windows features.

- **Driver and firmware updates**  
  Choose to manage updates automatically or manually. And control the flow of:
  - All drivers/firmware in a group or ring
  - Specific drivers/firmware across the tenant  
  - Drivers that previously couldn't be centrally approved

- **Microsoft 365 Apps for enterprise updates**  
  Autopatch ensures 90% of eligible devices stay on a supported version of the Monthly Enterprise Channel (MEC).

- **Microsoft Edge updates**  
  Autopatch aligns eligible devices with the Stable channel’s progressive rollout model.

- **Microsoft Teams updates**  
  Devices benefit from the standard automatic update channel for Teams.

- **Intune reports**  
  Monitor endpoint health and activity using native Intune reporting capabilities.

- **Hotpatch quality update report**  
  View policy-level update statuses for all devices that receive hotpatch updates.

- **Enhanced Windows quality and feature update reports & device alerts**  
  Identify and remediate devices that are not up to date, with alerting to help bring them back into compliance.

---

## Make updating easier!

Windows Autopatch is designed to make updating simpel for IT administrators by offering an automated, streamlined experience in a single pane view within Microsoft Intune. Over the last few updates, Microsoft has introduced significant enhancements to the platform to make it more efficient, secure, and user-friendly.

### No more activation required

Previously, administrators needed to activate certain features manually within the Microsoft Intune console. Now, this activation process has been retired, making features such as Windows Autopatch groups, reporting, and other tools available and easier to manage. This streamlines tasks like setting up rollout groups, configuring update policies, and monitoring update compliance. Gone with the hassle!

## Improvements

### April 2025 Improvements

With the April 2025 release, Windows Autopatch introduced three major improvements:

- **Enhanced Reporting**: Now covers all Intune-managed devices with client to cloud latency reduced to under four hours, categorizing devices into 'Up to date', 'In progress', or 'Not up to date', with historical tracking and insights.
- **More Flexible and Intelligent Groups**: No more shared policies between groups, allowing greater flexibility and control over which update content types apply to which devices.
- **Least-Privilege Access Model**: Windows Autopatch now operates with the permissions of the currently signed-in user, removing the need for the service to have full Intune administrator permissions, thus improving security and simplifying setup.

These updates are rolling out as we speak and aim to boost the security, flexibility, and ease of use of Windows Autopatch.

### Improved Reporting and Troubleshooting (June 2025)

Starting in June 2025, Windows Autopatch offers enhanced control over data sharing and troubleshooting capabilities:

- **Reporting and Alerting**: Managed via diagnostic data settings. Even if diagnostic data is disabled, devices still appear in reports, but with some data missing and alerts notifying admins.
- **Improved Troubleshooting**: The Windows Autopatch client broker can now be targeted selectively, helping diagnose update issues, such as detecting devices sourcing updates from outdated locations.

If the service cannot access essential information, it will now alert administrators, enabling better control and transparency.

### Hotpatching for Windows Client Devices

Hotpatching is now supported, allowing critical Windows security updates to install monthly without requiring a restart, which is great! This helps maintain security while avoiding interruptions to users. Requirements for enabling hotpatching as of the latest information include:

- Latest hotpatch baseline security update installed (quarterly releases, with April being the latest and July the next).
- Windows 11, version 24H2 for x64 (AMD and Intel) CPUs.
- VBS (Virtualization Based Security) enabled and running.
- CHPE disabled for Arm64 devices (hotpatching for these devices remains in public preview).

## Benefits for Organizations

- **Enhanced Security**: Regular updates reduce vulnerabilities, protecting against potential threats.
- **Operational Efficiency**: Automating the update process and have monitoring on the results of it give overview. This gives you more time to focus on strategic initiatives rather than routine maintenance.
- **User Productivity**: By minimizing disruptions during update deployments, users experience fewer interruptions, and maintaining continuity.

## Getting Started with Windows Autopatch

To start using Windows Autopatch, your organization must meet a few key prerequisites. Microsoft has integrated Autopatch directly into Intune, allowing IT teams to set it up with minimal effort.

### Prerequisites

Before enrollment, ensure the following requirements are met:

- **Licensing**: Devices must be licensed under one of the supported plans:
  - Microsoft 365 Business Premium
  - Windows 10/11 Enterprise E3/E5 (via M365 E3/E5, F3)
  - Education A3/A5, or Enterprise VDA licenses

- **Device Configuration**:
  - Devices must be **Azure AD-joined** or **Hybrid Azure AD-joined**
  - Managed via **Microsoft Intune**
  - Running a supported version of **Windows 10 or 11**

- **Security Requirements (for hotpatching)**:
  - Windows 11, version 24H2
  - Virtualization-Based Security (VBS) enabled
  - Devices must be compliant with Microsoft’s hotpatch baseline

### Onboarding Steps

1. **Check eligibility**: In the Microsoft Intune admin center, navigate to *Tenant Administration > Windows Autopatch* and review readiness status.

2. **Assign devices to Autopatch Groups**:
   - Autopatch automatically creates deployment rings
   - You can also create custom Autopatch Groups for departments or locations
   - Registering the devices can take up to 48 hours

3. **Review and customize policies**:
   - Adjust quality and feature update policies
   - Define rollout waves, driver handling, and hotpatch inclusion where supported

4. **Monitor update progress**:
   - Use the built-in **Intune reports** under *Reports > Windows Autopatch* to track compliance, performance, and troubleshooting alerts

### Best Practices

- **Pilot first**: Use the ‘Test’ ring for a small group of IT-managed devices to validate update behavior before wider rollout.
- **RBAC and Access Control**: Use for example PIM to assign the Intune Service Administrator role when configuring.
- **Update Monitoring**: Pair with **Update Compliance** or **Microsoft Defender for Endpoint** for additional monitoring. For example Vulnerability management and Exposure Management within the Defender portal.


## Conclusion

Windows Autopatch is a major improvement in IT management that makes keeping systems updated much simpler. By handling updates automatically, it frees IT teams to focus on other work instead of routine maintenance.

The 2025 updates including hotpatching without reboots, better reporting, and improved security access controls show that Microsoft is serious about making updates both secure and less disruptive. For companies struggling with patch management, Autopatch offers a solid solution that balances security with keeping operations running smoothly.

**Organizations using Windows Autopatch can expect:**

- Fewer security gaps through regular updates
- Less work for IT departments
- Better experience for employees with fewer update interruptions
- Clearer visibility into update status across all devices
- Easier management through integration with Microsoft 365 tools
- For the best results, combine Autopatch with security monitoring tools and create clear processes for handling any exceptions during updates. Start with a small test group, check the results, and gradually expand as confidence grows.
- Consider integration with Vulnerability Management in your Defender portal

If you read this, you went through it all. Thanks for reading this blogpost!
