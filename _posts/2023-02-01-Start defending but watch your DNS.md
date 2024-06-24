---
title: Start defending, but watch your DNS
date: 2023-02-01
description: Once we start defending our environments, what is there to lookout for outside your Microsoft environment?
categories: [Domains,DNS]
tags: [azure,dns,spf,dkim,dmark]
media_subpath: /assets/img/defending
image:
  path: Defender.png
  width: 100%
  height: 100%
  alt: Azure defender in the wild
---

# Introduction

So, you and your organization are facing forward, ready to defend your environment from whats to come… good! But do keep in mind to watch your back. Why? Well let’s get started on that!

# DNS...its always DNS

With your Microsoft Defender in place, you are guarding the door. But what if the danger might reside within your walls? Think about this. The walls of your castle are as high, thick and safe haven as they are seen in the Lord of the Rings movies. Yet these walls can be destroyed with just one simple change...**DNS**.

## Hosting provider
In my opinion good security starts with your domain and a domain starts with a provider. Many organizations have bought their domain years ago and configured the desired DNS settings for their domain. After these settings were set in-place they continued doing business as usual. In the meanwhile, we faced many changes, seen all sort of new attacks. With these new forms of attacks, we also found countermeasures which is **Multi-Factor-Authentication (MFA)**.

## Configure MFA
When you have access to your domain provider account, login and see if you have either MFA enabled, or see if your provider has access to this method. It is very **important** to keep your domain safe but also your DNS configurations which are making sure your e-mails are being delivered to your Microsoft environment! If your provider does not have any security tools in-place, consider contacting them to ask for these security features or move your domains to another provider which does have these options.

Use for example the [Microsoft Authenticator app](https://support.microsoft.com/en-us/account-billing/download-and-install-the-microsoft-authenticator-app-351498fc-850a-45da-b7b6-27e523b8702a){:target="_blank"} to add these accounts. It can be easily done by scanning the QR-code or manually fill a code to add the account to the authenticator. 

## Risks of domain hijacking

**Without** multifactor authentication in place on the account of your hosting provider, your domain is vulnerable to hijacking. If attackers gain access to your domain account, they would be able to change the **MX records** of your domain. This would allow the attackers to capture e-mails, gain more information or even access to accounts which use e-mail password reset verification. Also, your website can be taken down or redirected to a malicious page.

For these reasons, it is important to have multifactor authentication in place. This will help ensure your domain is and stays as secure as possible and reduce the risk of being victim of domain hijacking.

---

# Other usefull DNS configurations

## SPF (Sender Policy Framework) 

SPF is a protocol used to prevent email spoofing by verifying your domain to ensure that the email is indeed sent from your domain it claims to be sent from. An SPF record is published in the domain's DNS (Domain Name System) and specifies which IP addresses or hostnames are authorized to send email.

How can you change this and make sure all your e-mails are validated correctly? 
The first step is to find out if there are any other software packages which sends e-mails on behalve of your domain. This is important because if you have send mail to your customers through the use of this software, it probably ended up in their spam-folder anyway. Not very effective! 

But you, the defender, the IT expert can fix this! Find all the used software packages, e-mail environments that are currently being used in your organization, even printers. OK enough about printers.
Once you have collected the software inventory its time to collect ip-addresses or hostnames. This can mostly be found in the documentation pages of the software. Now how can you make this work with your SPF record.

**Lets grab a SPF record and break that up.** 

```
"v=spf1 mx include:spf.protection.outlook.com -all"
```
In the record shown above we see “**v=spf1**” which indicates that we are going to use the SPF-protocol. The “**mx**” tells that all the mails send through the given mx are accepted. 

> Now if your website is hosted elsewhere and your contact form messages does not seem to be delivered, add an “**a**” to add the ip-address stated in the A-record of your domain. This way it will accept messages coming from the ip-address of the A-record which is your website. 
{: .prompt-tip }  


Here comes the part where we can add more sources. The “**include:**” is a conditional which is being added to the whole SPF. So lets say you have two pieces of software which sends e-mail from their own server, but are using your domain. We add both the server hostnames or the SPF zone to the SPF. With the use of a hostname it is required for the server to do a lookup. A lookup is done to ask other DNS servers what the ip-address of mailserver.softwarecompany.com. The limit on these lookups is 11. 
To avoid such counts, we can also fill the direct ipv4 addresses to escape the need for lookups. This can be done by adding “**ip4:**”. 

The last bit is “**-all**” the – sign means that it’s a hardfail. Might a message fail to validate correctly it will be denied instantly. This setting is the best in my opinion due to the fact it gives instant action. With the use of ~ this would fail but delivers the message. To protect your users, mails should be validated. 
Let’s complete a SPF record with what we have read above. 


```
"v=spf1 a mx include:spf.protection.outlook.com include:mailserver.softwarecompany.com ip4:33.19.118.128 ip4:186.111.219.171 -all"
```

Once you are satisfied with the additions done to the record we can set it up in your domain configuration. Login to your hosting provider and go to its DNS settings. Once there, create a new TXT record or if there already is one, use that one instead. 
Fill the TXT record with the spf record you just made and save the record. Once the record is live it will actively validate e-mails from your domain!

In my next blogpost I will explain more about Defender for Office, DKIM and DMARC.







