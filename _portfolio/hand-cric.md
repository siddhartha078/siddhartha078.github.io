---
title: "Hand Cricket Game"
excerpt: "A fun CLI hand cricket game built in Python using loops, conditionals, and random module. Toss, two innings, and results — all in the terminal!"
header:
  image: /assets/images/headerhandcric.png
  teaser: /assets/images/headerhandcric.png
sidebar:
  - title: "Role"
    image: /assets/images/logo.png
    image_alt: "logo"
    text: "Solo Developer"
  - title: "Built With"
    text: "Python, Terminal (CLI)"
  - title: "Features"
    text: "Bat/Ball selection, innings logic, bot opponent, emojis, score calculation"
gallery:
  - url: /assets/images/terminalimage1.png
    image_path: /assets/images/terminalimage1.png
    alt: "User won the toss"
  - url: /assets/images/terminalimage2.png
    image_path: /assets/images/terminalimage2.png
    alt: "User batting gameplay"
  - url: /assets/images/terminalimage3.png
    image_path: /assets/images/terminalimage3.png
    alt: "Final score and result"
---

Hand Cricket is a simple CLI game where you play against a bot in a two-innings match. You toss, choose to bat or bowl if you win, and play by selecting numbers between 1 to 6 — with the bot randomly responding.

### Features
-  Toss logic with odd/even input  
> #### How it works
> You choose odd or even and then choose a number. If sum of the bot's choice number and the number you chose, is even, the person who chose even at the start will win the toss
-  Choice between Batting and Bowling  
-  Loops to simulate turns    
-  Game ends on matching numbers 
> i.e the batsman and the bowler choose the same number 
-  Score is compared at the end  
-  Emojis add extra fun!

{% include gallery caption="Gameplay screenshots from the terminal." %}
