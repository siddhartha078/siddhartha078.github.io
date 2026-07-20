---
title: "Weekly Blog 6"
date: 2026-07-20
layout: single
classes: wide
author_profile: true
comments: true
reddit_url: https://www.reddit.com/r/cybersecurityindia/comments/1v1p5ez/weekly_blog_6/
categories: [AWS, Cloud Service]
---

Couldn't do anything last week beacause college has started for us and the first week was a bit hectic. So, I'll be shifting to blog per 2 weeks now.

# From Linux to the Cloud: Making Sense of AWS IAM

I've spent the last while in the trenches of SOC work — writing detection rules, triaging alerts, digging through raw logs, chasing down attack techniques in Wazuh. All of that lives on Linux boxes with Linux permissions, Linux users, Linux logs. Comfortable territory.

The next step for me is AWS, and my account is still sitting in payment verification limbo (fun fact: even the free tier makes you prove you're a real person with a real card). So instead of waiting around, I started with the one thing that matters more than anything else in AWS: **IAM — Identity and Access Management**.

Here's the thing nobody tells you when you start cloud security: you already know most of this. It's just wearing a different costume.

## The Four Building Blocks

IAM boils down to four core concepts:

- **User** — a person or application with long-term credentials
- **Group** — a collection of users that share the same permissions
- **Policy** — a JSON document that spells out exactly what is and isn't allowed
- **Role** — like a user, but temporary. Something a service or person "assumes" for a limited time, then hands back

If you've ever managed a Linux box, none of this is actually new to you. It's a rename, not a reinvention.

## The Translation Table

Coming from Linux and Wazuh, here's how I've been mapping it in my head:

| Linux World | AWS IAM World |
|---|---|
| A user in `/etc/passwd` | An IAM User |
| A Linux group | An IAM Group |
| File permissions (`chmod`, `chown`) | An IAM Policy |
| `sudo` — temporary elevated access | An IAM Role |
| `audit.log` | CloudTrail |
| Wazuh alerting rules | GuardDuty |

The logic underneath is identical: **who is this, what are they allowed to touch, and can I prove it afterward?** Linux answers that with file permissions. AWS answers it with policies and CloudTrail. Same question, same instinct, different syntax.

This is just basics. But I'll go more deeper and learn it good. That's it for this week.

## Resources Used

- [Amazon AWS](https://aws.amazon.com/)
- My writeups at [Blogs](/posts/)
