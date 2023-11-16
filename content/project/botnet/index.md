---
title: A Stateless Heuristic Approach to Detecting Encrypted Botnet Command & Control Traffic Over Standard HTTP POST.
summary: Examination of Hypertext Transfer Protocol (HTTP) POST data to determine if it's feasible to differentiate legitimate traffic from botnet Command and Control (C&C) traffic without the need to decrypt said traffic.
tags:
  - Security
date: '2011-12-14T00:00:00Z'

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
url_pdf: "/uploads/paper_long.pdf"
# url_slides: ''
# url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

Abstract:
In this paper we examine Hypertext Transfer Protocol (HTTP) POST data to see if it is feasible to differentiate legitimate traffic from botnet Command and Control (C&C) traffic without the need to decrypt said traffic. The premise behind this approach is that C&C traffic will most likely occur in the body of a POST message and be encrypted at the application layer to avoid detection. Through heuristic analysis we demonstrate that it is possible to differentiate unencrypted traffic from encrypted traffic in a stateless fashion. Furthermore, we show that encrypted traffic, while similar to encoded traffic (such as Multipurpose Internet Mail Extensions (MIME) file uploads) is differentiable from legitimate traffic due to its length and a similarly encrypted response. The result of this research is the development of a theoretical understanding of a new method for detecting botnet traffic. The outcome is the development of a detection engine capable of this with both minimal false positive and false negative rates.