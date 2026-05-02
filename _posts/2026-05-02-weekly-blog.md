---
title: "Weekly Blog 1"
date: 2026-05-02
layout: single
classes: wide
author_profile: true
categories: [siem, linux, networking]
---

## Progress this week


#### Completed the **Linux Luminarium Dojo** at pwn.college

I got the linux badge (penguin) for completing it. The Dojo had around 130 challenges in all which gave me good idea of linux command sets and how to use them in different cases. The **Silly Shenanigans module** was kind of a headache but I did eventually got through it.

![Linux Luminarium](/assets/images/linuxluminaruim.png)

#### Successfully setup a **Home Lab** in VirtualBox

Used Kali linux and Ubuntu Server LTS 24.04 as the machines

#### Successfully setup **Wazuh** and added a simple rule and tested it.

- Wazuh is an Open-Source SIEM tool which manages all the security related events happening in your pc, sorted into different threat levels ranging from 0 - 16. I have installed it in my Ubuntu Server.
- I wrote a custom active response rule which blocks IP for 5 minutes if someone fails to ssh into the device for more than 8 times continuously. Mostly Bruteforce attacks happen this way and this is a good measure to minimize that. I tested it using **Hydra** tool in Kali Linux to the Ubuntu Server.
- The tool has successfully managed to block the IP of my Kali Linux (which was the attacker here) on its own for 5 minutes.

Wazuh Dashboard:
![Wazuh Dashboard](/assets/images/wzuh.png)

Wazuh Log:
![Wazuh Log](/assets/images/wzuhlog.jpeg)

#### Started learning OS and Networking

Learned about Process Management, the different states a process can be in etc and also learned about IPv4 Adresses, Subnetting, Supernetting etc.


## Resources Used

- [Wazuh](https://wazuh.com/)
- [pwn.college](https://pwn.college/)
- [Hydra](https://github.com/vanhauser-thc/thc-hydra)
- My writeups at [Blogs](/posts/)
