---
title: Offensive Cyber Hunting Deploying Deceptive Tools And Tactics
summary: A suite of tools developed which leverage deceptive techniques to discover attackers.
tags:
  - Security
date: '2017-09-20T00:00:00Z'

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
url_slides: '/uploads/deception.pdf'
# url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
url_slides: '/uploads/deception.pdf'
---

Overview:
A closed source project I developed while working for Tanium. The Deception Toolkit can deploy cross platform deceptive tokens anywhere across the enterprise in seconds to detect malicious activity, track, remove, and modify all of them in seconds.

The Deception content is currently comprised of:
Packages:
* Deception - Docx Token (Linux/OSX) 1 Deploy
* Deception - Docx Token (Linux/OSX) 2 Cleanup
* Deception - Docx Token (Windows) 1 Deploy
* Deception - Docx Token (Windows) 2 Cleanup
* Deception - Credential Memory Injection (Windows) 1 Deploy
* Deception - Credential Memory Injection (Windows) 2 CleanUp
* Deception - MiTM LLMNR/NetBIOS (Windows) 1 Deploy
Sensors:
* Deception Token Files
* Deception Memory Injected Credentials

Tech Stack:
The packages and sensors use python, Tanium is used for deployment and python and splunk are used for automation and correlation actions.