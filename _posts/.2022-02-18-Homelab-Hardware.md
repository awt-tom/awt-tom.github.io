---
title: The Homelab
date: 2022-02-18
categories: [Homelab, Hardware]
tags: [homelab]     # TAG names should always be lowercase
img_path: /assets/screenshots/homelab
image:
  path: Dell-Poweredge-R720.jpg
  width: 100%
  height: 100%
  alt: The Dell PowerEdge R720
---

## What is a Homelab?
The Homelab, what is it and what is it good for I hear people say. 

Well, a Homelab is basically a "Playground" or "Sandbox" where you run your own hardware with almost endless possibilities. 
It is also a safe place to fail on any experiment that you wouldn’t perform in a production environment. As you fail, you learn, you discover. You can use that knowledge into good use at work or friends who also work in IT. 

To me the Homelab is an environment where I can run what I want, the way I want. That way I created separated environments to work with. I have my production which is used for daily applications and services to use, Development to code and build functions for applications or games. Then there is the sandbox. The sandbox is used for pen testing. In this environment I use virtual machines with Kali, Windows server, Windows 10, Linux and several other operating systems. 

---

## Passion for Homelabs

For me it started early on. The internet made its big steps and online games came to live. As a child it was not that easy to get access to hardware and connectivity with such proportions to host a game server for an entire group of friends.  Luckily my dad had a strong interest in IT that time. With the hardware he wouldn’t use I made a second computer and started right off. Building my first HTML based website, hosting a “Habbo Hotel” web server were kids from school could join on without having to pay for certain objects or services. Setting up a server for the all famous “Battlefield” and loads of other fun things! 

It made things possible the way you and your friends prefer to play, with your own set of rules.

Now that I’m older the game servers are still there and are used from time to time. In the following years I became more and more interested in the way these services work and wanted to know more about them. I would search the internet to read about it, try them out and succeed or fail setting it up. Whenever I failed it could take a few nights in order to solve the issue, but oh boy did we get allot of knowledge out of those nights. Not to start about the feeling when it finally works… Awesome!


Anyway! We drift off from the subject; Homelabs!

Since me and my wife moved into our current house back in 2020 I had more space to work with. I started small with a spare computer I had and the oldskool feeling came right back at me. That feeling of full focus, a lot of nightly spend hours.


Last year (2021) I got myself an Intel NUC, great small computers to host smaller jobs such as pi-hole or Portainer with applications in container form. Although this was a great addition to the hardware team I found it was time for something bigger. I had the space, condition were nice and was ready to put some effort in building that Homelab I dreamed about. 

---

## The Hardware

I started of hunting for a rack. Would I need a big, medium or small rack. In the end I went for the medium version which I found on the marketplace. 

Luckily a friend of mine was near this location at the other end of the country, and he was driving a van with enough space to fit this rack in. Which resulted in a quick pick-up which I am still thankful for! 

![Desktop View,img-description](Server-rack.jpg){: width="700" height="400" }
_The new serverrack in the garage_

There it was, the start of the Homelab!
Now onto the more fun hardware part, the server!

My colleague, friend and homelab buddy Mikey had a spare server for sale. It was a Dell Poweredge R720, which was an amazing start for this lab!

![Desktop View,img-description](Dell-Poweredge-R720.jpg){: width="700" height="400" }
_The Dell Poweredge R720_

It contained the following parts

| **PART**  | **TYPE**  | **SPEED**  | **SIZE**  |
|---|---|---|---|---|
| **CPU**  |  2x E5 2650 V1 | 2.00GHZ  | 20MB Cache |
| **RAM**  |  Mixed ECC | 1066mhz | 68 GB  |
| **DRIVES**  | SAS  | 10K  | 5x 300GB |

Soon after the initial setup I bought some new parts and added a spare SSD to upgrade the current hardware. 

| **PART**  | **TYPE**  | **SPEED**  | **SIZE**  |
|---|---|---|---|---|
| **CPU**  |  2x E5 2690 V2 | 3.00GHZ  | 25MB Cache |
| **RAM**  |  Mixed ECC | 1866mhz | 128 GB  |
| **DRIVES**  | SAS  | 10K  | 5x 300GB | 
| **SSD-DRIVES**  | SSD  | EVO  | 1x 250GB | 

Currently the rack has been a new patch panel and a Ubiquiti Dreammachine.

Since the begin of 2023 I upgraded the server with a PCI card which is loaded with a Samsung 980 SSD 1TB.


