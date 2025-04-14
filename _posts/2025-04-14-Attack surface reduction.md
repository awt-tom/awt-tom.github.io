---
title: Implementing Attack Surface Reduction Policies
date: 2025-04-14
description: Start implement Microsoft's Attack Surface Reduction (ASR) policies today!
categories: [Defender, ASR]
tags: [attack surface reduction,security hardening,asr, ] # TAG names should always be lowercase
media_subpath: /assets/img/asr
image:
  path: asrbanner.png
  width: 100%
  height: 100%
  alt:
---
# Why Attack Surface Reduction is mandatory in every Organization

In today’s threat landscape, **prevention is everything**. While detection and response are crucial, reducing the opportunities attackers have in the first place is without doubt even more important. This is where **Attack Surface Reduction (ASR)** comes in, a set of controls in **Microsoft Defender for Endpoint** designed to harden endpoints and reduce the attack vectors available to malicious actors. This targets behavior that malware and malicious apps use to infect computers.

So before you dive deeper into all the other awesome security features, make sure you've got **your own Attack Surface Reduction configured**.

---

## What is Attack Surface Reduction (ASR)?

ASR provides a **set of rules** that block actions typically used by malware, even if that malware hasn’t been seen before. Think of it as proactive hardening, blocking risky behaviors like:

- Executables launching from email or Office files  
- Scripts executing from temp folders or downloaded content  
- Office apps creating child processes (like `PowerShell` or `cmd.exe`)  

Each rule targets a specific tactic attackers use. These actions can be **audited** or **blocked**, and Microsoft regularly adds new rules as new threats emerge. When implementing ASR, be sure to stay up to date and adjust your rule configure new rules as they are being added.

---

## Why ASR is essential

Too many organizations still rely on **EDR (Endpoint Detection and Response)** to investigate *after* an attack has landed. Although EDR adoption is growing, there are features like **Attack Disruption** and **ASR** that can **prevent attacks before they execute**.

Especially in phishing scenarios, ASR rules can be the difference between a **blocked attack** and a **ransomware Massacre**. Implementing these features means stopping malicious activities **before** tools like Microsoft Sentinel even begin log correlation.

---

## What kind of rules are there?

Here are the current **ASR rules** available for configuration:

- Block abuse of exploited vulnerable signed **drivers**  
- Block **Adobe Reader** from creating child processes  
- Block all **Office** applications from creating child processes  
- Block credential stealing from the **Windows local security authority subsystem** (lsass.exe)  
- Block executable content from **email client and webmail**  
- Block executable files from running unless they meet a prevalence, age, or trusted list criterion  
- Block execution of **potentially obfuscated scripts**  
- Block **JavaScript or VBScript** from launching downloaded executable content  
- Block **Office applications** from creating executable content  
- Block **Office applications** from injecting code into other processes  
- Block **Office communication application** from creating child processes  
- Block persistence through **WMI event subscription**  
- Block process creations originating from **PSExec and WMI commands**  
- Block rebooting machine in Safe Mode  
- Block untrusted and unsigned processes that **run from USB** 
- Block use of copied or impersonated system tools  
- Block **Webshell creation** for Servers  
- Block Win32 API calls from Office macros  
- Use advanced protection against ransomware

> Microsoft regularly adds new rules as new threats emerge. When implementing ASR, be sure to stay up to date and adjust your rule configure new rules as they are being added.
{: .prompt-tip }

### Each rule can be set to:
- **Not Configured** (Call to action)
- **Off** (Also a call to action)
- **Block** (Where you want to be at)
- **Audit** (Recommended starting point)
- **Warn** (This will block the action, but lets the user decide to bypass)

---

## Microsoft Defender Antivirus Exclusions

If you exclude files from **Defender Antivirus**, **ASR rules may still block them**. Not all rules use the Antivirus exclusions.

Here are the rules that **do NOT use Defender AV exclusions**:

- Block Adobe Reader from creating child processes  
- Block process creations originating from PSExec and WMI commands  
- Block credential stealing from the Windows local security authority subsystem (lsass.exe)  
- Block Office applications from creating executable content  
- Block Office applications from injecting code into other processes  
- Block Office communication application from creating child processes  

If you *must* exclude files for these rules, do it **within the ASR rule itself**.

---

## Defender for Endpoint Indicators of Compromise (IOC)

You might wonder, **what are IOCs**?

**Indicators of Compromise** are bits of information shared and detected by Defender for Endpoint, such as:

- Hashes of known malware  
- Malicious IP addresses  
- Domains or URLs that distribute malicious content  
- Certificates  

However, **some ASR rules do not use IOCs**, such as:

| ASR Rule                                      | IOC Not Used              |
| --------------------------------------------- | ------------------------- |
| Block credential stealing from lsass.exe      | Files and/or Certificates |
| Block Office applications from injecting code | Files and/or Certificates |
| Block Win32 API calls from Office macros      | Certificates              |

---

## Where to Start?

Let’s start simple. Use the information above to evaluate the **impact** of enabling ASR.

We want to test potential impact on your environment by running rules in **Audit mode** via Intune:

> Hold your horses: Before continuing to the next step. Make sure that your Defender portal is connected to Microsoft Intune and that your devices are being onboarded so that Microsoft Defender for Endpoint is present.  
{: .prompt-warning }

### Steps to Configure ASR in Audit Mode:
1. Go to [Intune](https://intune.microsoft.com)  
2. In the left menu, click **Endpoint Security**  
3. Select **Attack Surface Reduction**  
4. Click **Create Policy**  
5. Choose platform: **Windows**  
6. Profile: **Attack Surface Reduction Rules**  
7. Click **Create**  
8. Name the policy, for example `ASR – Audit mode`  
9. (Optional) Add a description
10. Set **all rules to "Audit"**  
11. (Optional) Add tags  
12. Assign to **all devices** for data collection  
13. On the **Review & Create** page, click **Save**

### What Happens Next?
- Policy will be pushed to all assigned devices.  
- Devices will report potential blocks to the **Defender portal**.  
- To test manually, open the **Defender menu** in your taskbar tray > check **history** of blocks.  
- You’ll see paths and files that *would* have been blocked.

> Let the policy run for a few days up to a few weeks to gather enough insights.
{: .prompt-info }

---

# Scoping ASR Correctly

**Scoping** ASR policies correctly is **crucial** to ensuring that your security measures are effective without creating **gaps**. When assigning devices to ASR policies, it is important to consider what kind of exclusions are being made. For example, the finance department might require certain exclusions due to the **nature of their work** and the types of applications they use. However, these exclusions may not be necessary for other departments, such as marketing or HR.

By applying exclusions across **all devices**, you risk creating security gaps where they are not needed, and therefore lack the overall effectiveness of your ASR policies. Each department has unique requirements and potential threats, so it is essential to consider the scope of your ASR rules to match these **specific needs**.

Another thing to keep in mind is the way you **exclude certain files**. Try to **avoid excluding complete folders** which has the recursive effect. For instance, excluding entire directories, such as `C:\Users\*\AppData\Local\Temp\*`, can provide a haven for malicious software to **operate undetected**. This not only impacts the effectiveness for your ASR rules, but also **open the door** for widespread security breaches in many cases.

So again, start of with **auditing your environment** as explained before. **Gather that information** and exclude where it is **only really necessary**. This way you can provide every department with a policy and being able to have better control on necessary exclusions without assigning them to all your devices.

---

## The Danger of Wildcard Exclusions

As said before exclusions can help you avoid operational impact, but used incorrectly, they can be a great tool for threat actors to use. Some examples:

```
C:\Users\*\AppData\Local\Temp\*
```

Or worse:

```
C:\*\*\*
```

Other case where folders have different versions.  
Original path of potential block in audit modus:
```
C:\Program Files (x86)\Microsoft\Edge\Application\135.0.3179.66\Installer
```

Path with added wildcard exclusion:

```
C:\Program Files (x86)\Microsoft\Edge\Application\?\Installer
```

See where this is going?

These wildcard exclusions (using * and ?) can easily be exploited. If malware lands in a folder that’s excluded with a wildcard, ASR won’t stop it, even if the behavior is clearly malicious.

**My advice**: avoid wildcards unless absolutely necessary, and always monitor excluded paths for abuse.

---

## Audit reports

In the early days of ASR we had to use KQL in order to see what kind of rules were being hit by certain files or software. Nowadays Microsoft made it easier for people to see these statistics by the rapport page. If you know KQL or want to start with it I encourage you to start use it. KQL really makes finding the specific information/situation easy, if you know its ways that is to say.   

To see the results of your earlier made policy to audit:

- Visit [security.microsoft.com](https://security.microsoft.com)  
- In the left panel go to “Reports”  
- Under “Endpoints” you will find “Attack Surface Reduction Rules”  
- On the filter page you will see “Rules: Standard protection” choose “All” to see all the metrics.  
- Choose a data according to what you want to view and filter on any selected rules if you wish to see a specific rule impact.

If the policy runs for a while on the user machine you should see some input now. This will be flagged as “Audited Detections”. This means that if the policy that got hit would be in block mode the user action would have been stopped. Use this metric to consider if this action was really necessary or that it could be blocked.

Some other usecases:

- You can also use this report to see trends in your organization. Use it at least once in a while to see what is happening.

- You can also see the configuration. This will state all the current configuration of devices in your environment. Great to see if all your devices are configured correctly.

- If you see a specific Audit/Block that you will need to exclude from the specific ASR rule, go to the “Add exclusions” page. Here you will see all the hits. By clicking on it you will see all the metrics and you will be able to download the paths which were involved.

For example you have checked if the software that has been hit by a rule requires an exclusion. You know that only the finance department is using this. You will then use the path to exclude this on the specific ASR rule that is being hit. And this is why it is important to have separated policies for every department/role to make sure only those who need it will get it.

---

## Final Thoughts

ASR isn’t just a “nice to have.” In 2025, it's mandatory for any organization that takes security seriously. If you’re not using it, you’re leaving the door open. And if you’re using it with a bunch of wildcard exclusions, you're leaving your door somewhat unlocked.

Start small, audit and gather information, start block future risks today!


