---
title: Optimize your SOC with SIEM and XDR Recommendations
date: 2025-01-09
description: Use the Microsoft XDR optimization feature to improve a unified SIEM and XDR environment
categories: [Microsoft Sentinel,XDR]
tags: [  
  microsoft sentinel,
  microsoft xdr,
  soc optimization,
  unified coverage management,
  siem and xdr integration,
  mitre att&ck,
  threat detection,
  detection rules,
  analytic rules,
  security configuration,
  spear phishing detection,
  initial access detection,
  microsoft defender portal,
  xdr coverage gaps,
  email security coverage,
  endpoint protection,
  siem recommendations,
  mitre framework
]
 # TAG names should always be lowercase
media_subpath: /assets/img/optimizeyoursoc
image:
  path: optimization_banner.png
  width: 100%
  height: 100%
  alt:
---
## Introduction

Microsoft has released a new unified coverage experience for SOC optimization. Previously, it was possible to get recommendations in Sentinel through the SOC optimization tab, which can also be accessed at [security.microsoft.com](https://security.microsoft.com){:target="_blank"}.

![Desktop View](SOC_optimization_button.png)

This feature provides an overview of what your organization currently covers through detection rules, policies, and other configurations.

---

## What is Unified Coverage Management?

As you might have seen, Microsoft now allows you to add your Sentinel workspace to the Microsoft Defender portal. With this in place It is now possible to view your coverage over your SIEM and XDR and see where you can find gaps in detection or configuration to improve in certain scenario’s.

This integration enables you to use the optimization to a better use:

- View your coverage across SIEM and XDR.
- Identify gaps in detection or configuration.
- Improve specific scenarios by enabling products (such as Defender for Endpoint), adding connectors, implementing new detection rules, or optimizing the sue of ingested data.

The great advantage is that suggested improvements are either ready to grab from the content hub or takes you to the Microsoft Learn page on how to implement a product. For example, you can:

- Access detailed content suggestions.
- Be redirected to Microsoft Learn pages for product implementation.
- Use the content hub to deploy specific detection rules.

It is now also possible to get coverages scores across all the data that is processed with your XDR & SIEM. That way you can receive highlights in the areas that you either have proper coverage or where improvements are highly advisable. 

![Desktop View](current-recommended.png) 

![Desktop View](different-view-indicator.png)

You can also click on the captions such as "Inactive products" and "Inactive products".

---

## How Does It Work?

The unified coverage management experience helps organizations close security gaps by leveraging the **MITRE techniques and tactics** displayed on the MITRE page in the Microsoft Defender portal. 

All recommendations are centralized in the coverage table on the MITRE ATT&CK page, which can be found under the Microsoft Sentinel tab in the Defender portal.

![Desktop View](MITRE_ATTCK_page.png)

Here, you can explore the MITRE ATT&CK framework and visualize paths related to specific threats.

---

### Threat Scenarios

One powerful feature is the ability to enable specific **Threat Scenarios**. These scenarios allow you to narrow down the view to techniques and tactics relevant to a particular threat type. This way you can avoid being bombarded by all the information which is shown in the framework that has nothing to do with the scenario you are looking for. 

![Desktop View](Enable_TS_MITRE.png)

This intergration enables you to:

- Identify coverage gaps at different attack lifecycle stages.
- Click on specific tactics to see detailed coverage per segment, such as:
  - Initial Access
  - Persistence
  - Credential Access

For example. Traditionally we would note down one of the MITRE formats. 

---

#### Example Scenario: Initial Access

**Tactic:** Initial Access  
**Technique:** [Spear Phishing Attachment (T1566.001)](https://attack.mitre.org/techniques/T1566/001/){:target="_blank"} 
**Description:** Adversaries may send emails with malicious attachments to exploit users and gain system access.  

**Detection Coverage:**
- **Endpoint Protection:** Partially covered.
- **Email Security:** Fully covered through Microsoft Defender for Office 365.
- **SIEM Alerts:** Available with relevant analytic rules in Microsoft Sentinel.

**Recommendations:**
- Enable anti-phishing policies in Microsoft Defender for Office 365.
- Create hunting queries in Sentinel to monitor suspicious email activity.

---

#### Why It Matters

Traditionally, validating if detection rules or policies were configured required creating validation tests through APIs or manually navigating portals. A time consuming process. By narrowing scenarios within the MITRE framework we can now see exactly per scenario what is configured/covered.

- Makes the validation process more efficient.
- Provides instant visibility into existing coverage.
- Highlights areas for future improvement.

This approach saves time, improves oversight, and ensures that your SOC is equipped to handle threats.

Here we can see that we do not have the products enabled and so we do not have the coverage we hoped for. By clicking "View all coverage details" we can see all the recommendations that we can use to cover certain situations.

![Desktop View](techniques_overview.png)

![Desktop View](full-threat-overview.png)

> Optionally you could grab the detection rule from the content hub, install them in your test environment and export them. You can then convert them with the tool as explained in my [earlier blogpost](https://azurewithtom.com/posts/Generate-ready-to-use-analytic-rules/){:target="_blank"} by adding a folder "Custom" to convert it to JSON format. It can than be deployed through the use of code.
{: .prompt-info }

## Conclusion
In this blog, we explored the new Unified Coverage Management experience for Microsoft XDR and Sentinel. We looked at how it provides actionable insights to optimize SOC operations, aligns with the MITRE ATT&CK framework, and introduces threat scenarios for more focused analysis. By leveraging these tools, organizations can enhance their detection capabilities, address security gaps efficiently, and stay ahead of cyber threats.Make sure to start exploring these features today to take your SOC to the next level!

> I advice to always think beyond a framework, but use it as a navigator to implement improvements. Always create your own scenarios based on your organization as not everything is covered in this feature. And maybe, maybe we get the option to share these own build scenarios as a community some day.
{: .prompt-warning }

