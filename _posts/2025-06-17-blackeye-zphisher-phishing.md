---
title: "Simulated Phishing Attack using BlackEye"
date: 2025-06-20
categories: [Labs, Phishing]
layout: single
classes: wide
author_profile: true
---

## Objective

Simulate a phishing attack using BlackEye on a local VM to understand how credential harvesting works.

---

## Tools Used

- BlackEye, Zphisher  
- Kali Linux(VM)  
- Localhost setup (VM)

---

## Steps

1. Cloned BlackEye, Zphisher repositories from GitHub
2. Launched the phishing page for Instagram,Netflix
3. Used a tunnel to expose localhost (Ngrok, localxpose, etc.)
4. Opened the phishing page on victim browser
5. Captured the login credentials in terminal

---

## Observations

- Most kits just use HTML/CSS clones of login pages
- BlackEye stores creds in plain text
- Some pages are broken/outdated

---

## Takeaways

- Never trust links — always verify domains
- Tools like these are good for **defenders to understand attacker techniques**
- Real-world phishing often uses shortened or hidden URLs

---

##  Resources

- [BlackEye GitHub](https://github.com/thelinuxchoice/blackeye)
- [Zphisher](https://github.com/htr-tech/zphisher)
- My writeups at [Projects](/posts/)
