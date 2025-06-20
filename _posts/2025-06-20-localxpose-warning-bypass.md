---
title: "Bypassing LocalXpose's Phishing Warning Page"
date: 2025-06-20
categories: [Labs, Phishing]
layout: single
classes: wide
author_profile: true
---

Observations found while trying Phising again

## Background

>During a phishing lab simulation, I used **LocalXpose** to expose my local phishing page to the internet. While testing, I noticed that LocalXpose displays a **warning page** before users are redirected to suspicious-looking URLs.
>
>But  That warning can be **bypassed.**

---

## What I Did

1. Hosted a phishing page using **Zphisher**
2. Used **LocalXpose** to tunnel the localhost to a public URL
3. Opened the public URL in incognito mode
4. LocalXpose showed a warning screen like:
   > "This site may be trying to phish credentials"

5. ✅ Observed that:
   > - The warning can be completely ignored if we attach a **/login.php** to the URL.
   > - In some devices if the victim clicked the warning and accepted once, **future visits went straight to the phishing page**

---

## Why This Matters

Phishing kits rely heavily on tunnels like Ngrok and LocalXpose. Warnings are meant to protect users — but this bypass means:

- A first-time victim could **land directly on the fake page**
- Social engineering ("Click once to continue") still works
- Attackers could test which clients/browsers show the warning and adapt

---

## Defensive Thoughts

- Always use browser isolation or test inside VMs
- Pay attention to even **legit-looking warnings** — they are your shield
- Developers of tunnel services need stricter warning enforcement

---

## My Takeaway

This shows how even safety features in good tools can have holes — and *any bypass* is worth documenting, because someday, **you’ll stop an attacker using it**.

---

## Tools Used

- LocalXpose
- Zphisher
- Kali Linux
