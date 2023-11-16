---
title: Security orchestration and automated response
summary: Automated Framework which provides risk scoring of users and systems as well as automated detection and response actions.
tags:
  - Security
date: '2017-09-27T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: ''
  focal_point: Smart

# links:
#   - icon: twitter
#     icon_pack: fab
#     name: Follow
#     url: https://twitter.com/georgecushen
# url_code: ''
# url_pdf: ''
url_slides: '/uploads/risk.pdf'
# url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
url_slides: '/uploads/risk.pdf'
---

Overview:
The security data analystics and risk correlation app is a full stack enterprise security solution that I developed during my time working with Tanium.

The app provides a scoring system for users and their machines based upon:
Risk Scoring:
* 20% - Tanium Comply Score
* 20% - Critical OS Patches
* 10% - 3rd Party App Versions
* 10% - Anti-Virus
* 10% - Tanium SOE/Health Check
* 10% - User Behavior Analytics
* 10% - Operating System Score
* 5% - Encryption
* 5% - Malicious Analytics

The app provides the following deliverables:
Actions:
* Automated Responses:
** Score > 80 = send alert
** Score > 50 + other alert = IR package deployed
** Score > 90 + other alert = Quarantine action
* Measure risk across multiple planes.
* Motivate users and system owners to reduce risk.
* Track improvement over time.
* Provide a single score for every user and every device.
* Enable senior management a conduit to support risk program.
* Inspire competition through gamification.

Tech Stack:
The packages and sensors use python, bash, and vbscript, Tanium is used for deployment and python is used for automation. Dashboarding is provided via splunk.
