---
title: Bringing Microsoft Sentinel Workbooks to the Microsoft XDR Portal
date: 2024-12-11
description: Microsoft has added the Microsoft Sentinel Workbooks to the XDR portal
categories: [Microsoft XDR,Workbooks]
tags: [sentinel,workbooks,xdr] # TAG names should always be lowercase
media_subpath: /assets/img/workbooktoxdr
image:
  path: workbookbanner.png
  width: 100%
  height: 100%
  alt:
---

### Bringing Microsoft Sentinel Workbooks to the Microsoft XDR Portal

Cybersecurity is changing fast, and it’s important to have all your tools and insights in one easy-to-use platform. Microsoft has been working on this with Microsoft XDR, a versatile tool that makes detecting and stopping threats simpler. Although many features have been added to the XDR portal, Microsoft Sentinel workbooks were only available in Sentinel. Now, that’s changed. You can use Sentinel workbooks directly in the XDR portal!

> If you have not intergrated your Sentinel workspace to Microsoft XDR it will not be possible to see this tab, and you will not be able to see the workbooks. Intergrating is easy and does not take much time. Go to the home tab of the XDR portal and click on the intergration of Sentinel. You will either need "Owner" permissions or "Sentinel Contributor" and "User Access administrator".
{: .prompt-info }

#### Why Sentinel Workbooks Matter
Microsoft Sentinel workbooks are a great addition to your threat monitoring and investigations. These highly customizable, interactive dashboards allow security teams to visualize telemetry, track key performance indicators such as analytic rules, and hunt for threats with precision. From displaying log analytics data to illustrating alert trends, workbooks are a must have for day-to-day security operations.

Yet, without native integration into the XDR portal, security teams must jump multiple portals, toggling between Sentinel and XDR environments to access workbook insights. This jumping experience can result in inefficiencies and delays in critical threat detection processes. In my personall case, i'd like it to have it all in one single pane. 

#### New Possibilities with Integration
When you have integrated your Microsoft Sentinel workspace in the Microsoft XDR portal, it is possible to work directly with Sentinel within the portal. With this feature, a whole new range of possibilities opens up. A recently added feature is the ability to directly open workbooks to see the information you need to hunt threats or to gain better insights into what is happening in your environment.

To access this feature:

- Open the Microsoft XDR portal at [https://security.microsoft.com](https://security.microsoft.com){:target="_blank"}.
- Navigate to the tab “Microsoft Sentinel.”
- Under “Threat Management,” click on “Workbooks.”
- You will see the new workbook page where you can view your current workbooks and add new ones to enhance your toolbox.

![Desktop View,img-description](workbookpage.jpg)

- Click on “Templates” and select a template you’d like to view.
- Click “Save” to add the workbook to your “My Workbooks” view or choose “View Template” to preview its content.

![Desktop View,img-description](saveworkbook.jpg)

- When saving a workbook, you’ll be prompted to choose the region where you want to store it.

> You can also create your own workbooks by adding your favorite KQL queries to design customized overviews tailored to your needs.
{: .prompt-info }

Once the workbook is added, you’ll be able to have all your favorite workbooks in one spot. 

![Desktop View,img-description](addedtooverview.jpg)

- Select a workbook and click “View Saved Workbook” in the side panel to see real-time insights.

![Desktop View,img-description](viewsavedworkbook.jpg)

This example is the most simple workbook to access. There are many more complex KQL workbooks out there in the community's.

![Desktop View,img-description](partofworkbook.jpg)


#### All Your Workbooks in One Place
Imagine a scenario where every Sentinel workbook is accessible directly within the XDR portal. By centralizing these tools, security teams could:

- **Enhance Visibility:** Gain a better view of all telemetry and alerts in one unified interface, eliminating the need for platform-switching.
- **Streamline Threat Hunting:** Use XDR’s advanced hunting tools in combination with Sentinel workbooks to correlate data across endpoints, identities, and cloud assets with ease.
- **Improve Collaboration:** Work better together among security team members by unifying investigative workflows in the XDR environment.
- **Increase Efficiency:** Save time by managing workbook configurations, data sources, and visualizations without leaving the XDR portal.
- **Community involvement** Within the Microsoft CyberSecurity community's there are alot of members who activly share insights and queries for your workbooks to use. Give them a shoutout and maybe share your own insights to the community!

#### Overcoming Challenges
While the benefits of such an integration are clear, implementation requires thoughtful planning.

- Ensure data integrity and seamless migration between platforms.
- Maintain the customization capabilities of workbooks within the XDR portal. It keeps getting better, easier.
- Provide training and documentation to help security teams adapt to work with workbooks and understand the underlaying data.

#### Looking Ahead
The integration of Sentinel workbooks into the Microsoft XDR portal is a step forward in unified security operations. By bringing these tools together, Microsoft helps organizations to detect, investigate, and respond to threats faster and more effectively than ever before.

A "single pane of glass" approach is not just a convenience; it’s a must for staying ahead of cyber threats.

> If you made it this far reading, thank you! If this helped you, please share it with your fellow security enthusiasts!
{: .prompt-info }

