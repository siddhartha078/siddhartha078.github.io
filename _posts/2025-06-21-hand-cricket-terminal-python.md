---
title: "Building My First Terminal Game in Python: Hand Cricket 🏏"
excerpt: "I created a basic hand cricket game using just Python and the terminal. Here's how I built it, what I learned, and what I plan to improve."
date: 2025-06-21
categories: [Devlog, Projects, Python]
author_profile: true
header:
  image: /assets/images/headerhandcric.png
  
---

## Why I Built This

I've recently been diving into Python, and while doing random beginner projects, I wanted to build something that I actually played as a kid — like **Hand Cricket**

So I ended up creating a small terminal game where I (the user) face off against a bot in a match of tosses, batting, bowling, and randomness.

---

## What It Does

It’s a basic **command-line cricket match** between me and a bot:

- Toss by choosing odd or even
> ### How it works
> You choose odd or even and then choose a number. If sum of the bot's choice number and the number you chose, is even, the person who chose even at the start will win the toss
- Option to **bat or ball**
- You keep hitting until you're out (when numbers match)
> i.e the batsman and the bowler has to choose the same number
- Two innings: whoever has more score wins

It has:
- `input()` for all user actions
- `random.choice()` for bot decisions
- Emoji-based results for fun
- A lot of simple `if-else` and `while` logic

---

## My Code Structure

I didn’t use any advanced libraries. Just:

```python
import random
```

Check my portfolio for the link: [Portfolio](/portfolio/)