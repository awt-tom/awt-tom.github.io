---
title: Generate ready to use analytic rules
date: 2024-06-23
description: We will use a script I recently created to generate a set of analytic rules, ready to be used in Microsoft Sentinel.
categories: [Microsoft Sentinel,Analytic Rules]
tags: [  
  microsoft sentinel,
  analytic rules,
  powershell script,
  yaml to json,
  sentinel automation,
  sentinelarconverter,
  azure sentinel github,
  arm templates,
  security rule conversion,
  sentinel deployment,
  detection rules,
  azure devops integration,
  security as code,
  kql rules,
  detection engineering,
  cloud security automation,
  yaml conversion
]
 # TAG names should always be lowercase
media_subpath: /assets/img/massyamltojson/
image:
  path: script_afbeelding.jpg
  width: 100%
  height: 100%
  alt:
---

## Introduction

When I started exploring Microsoft Sentinel I started to find out that managing and **enabling detection rules** can be quite the job. Especially when you had to do this for multiple environments.

We could either install one of the now used solutions in the content hub to get rule templates. But this will still require you to enable the rules and take certain steps in order to get them working. Importing rules one by one was also a very time consuming task. 
Along the way I tried many things that suited my situation to get a good start in enabling detections and being able to update them.

Fellow tech enthusiasts and friend **[Fabian Bader](https://cloudbrothers.info/en/aboutme/){:target="_blank"}** has created a great Powershell module called **[SentinelARConverter](https://github.com/f-bader/SentinelARConverter){:target="_blank"}** which has the possibility to convert Analytic rules in **YAML** form to **JSON**. This is especially useful to convert them in a way that they can be used to import the Analytic Rules with the use of Powershell.

Because I wanted to run multiple conversions and to be able to get the most recent version of detection rules I created a script. The script uses this tool and is able to grab the YAML files from the **Microsoft Github repository** which contain **Analytic rules** by **Solution name**.

## Overview

This PowerShell script automates the process of downloading YAML files from the Azure Sentinel GitHub repository which contain analytic rules, converting them to JSON format, and saving them locally in their original folder structure. 

This way the Analytic rules are all sorted per solution which makes it easier to pick these rules based on their solution name. The Analytic rules are ready to be used and can straight up be used to import  them in Microsoft Sentinel. Adding the rules to for example Azure Devops or Github makes it possible to deploy all the analytic rules at once.

You can find the script in my [Github page](https://github.com/awt-tom/mass-yaml-to-json){:target="_blank"}


## How does it work?

This PowerShell script, `Convert-YamlToJson.ps1`, is a tool for Microsoft Sentinel Security engineers who manage Microsoft Sentinel's Analytic rules. Here’s what you can do with a simple command line:

- **Standard run**: `.\Convert-YamlToJson.ps1`
- **Show folders that do not contain any Analytic Rules**: `.\Convert-YamlToJson.ps1 -NoARfolders`
- **Define other locations**: `.\Convert-YamlToJson.ps1 -RepoUrl "https://github.com/Azure/Azure-Sentinel" -SourceRoot "C:\temp\Azure-sentinel\Solutions" -DestinationRoot "C:\Convertedrules"`

### **Description**

The script automates several crucial tasks:
- **Clones or updates the specified Azure Sentinel GitHub repository**.
- **Converts YAML files related to analytic rules into JSON format**.
- **Saves the JSON files to a specified local directory**, maintaining the original folder structure.
- Optionally, **displays folders that do not contain any analytic rules**.

### **Parameters**

- **RepoUrl**: The URL of the GitHub repository. Default is `https://github.com/Azure/Azure-Sentinel`.
- **SourceRoot**: The local path where the repository content will be stored. Default is the `Solutions` folder under `Azure-sentinel` in the temp directory.
- **DestinationRoot**: The local path where the converted JSON files will be saved. It defaults to the current working directory with a subfolder named `Converted_rules_<current_date>`.
- **NoARfolders**: A switch to show all folders that do not contain any Analytic Rules.

### **Example Usage**

```powershell
.\Convert-YamlToJson.ps1
```

### **Prerequisites**

- **Git**: Ensure Git is installed and available in the system path. Download from [git-scm.com](https://git-scm.com){:target="_blank"} and follow installation instructions.
- **PowerShell Execution Policy**: Set to allow running scripts, e.g., `Set-ExecutionPolicy`.
- **SentinelARConverter Module**: Required for converting formats; the script will ask to install it if not found.

### **Supported Terminals**

The script is compatible with:
- **Windows PowerShell**: The default environment in Windows.
- **Windows Terminal**: Supports multiple tabs and profiles.
- **Visual Studio Code**: Run scripts using the integrated terminal.
- **PowerShell ISE**: A graphical host for PowerShell included with Windows.

### **Script Details**

- **Git Check and Installation**: Verifies and installs Git if necessary.
- **SentinelARConverter Module Check**: Ensures the converter module is installed, installing from the PowerShell Gallery if absent.
- **Cloning or Updating Repository**: Manages repository updates or initial cloning.
- **Converting YAML to JSON**: Iterates through folders, converts files, and saves them appropriately.
- **Logging and Progress**: Includes a progress bar and logs for tracking.
- **Summarizing Results**: Provides a terminal summary of conversion successes and failures.

## Demo video
{% include embed/youtube.html id='dJObJJQ9o0g' %}



> ### Keep track of changes
Analytic rules tend to change and update once in a while. While the script grabs the latest Analytic rules from the Github page does not always mean that they are the best to use. 
Make sure to try them out in for example a test environment, or if you feel KQL Capable read the query's and split view the changes.
{: .prompt-info }


## Whats next?

I am sure there are many improvements to be made to the script and that there is a potential to new functions. I am open to any suggestions made and will try to do my best to it where ever I can.

**Improvements:**
- Add a log file for failed conversions
- Scope to user

**Other idea's:**
- Filtered Version
- Pipeline Version
