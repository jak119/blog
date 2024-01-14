---
title: "Exclude a Specific Path in Cloudflare Zero Trust"
categories:
  - SelfHosting
tags:
  - cloudflare
  - cloudflare teams
excerpt_separator: <!--more-->
toc: false
---

To exclude a specific path in Cloudflare Zero Trust (e.g., the share URL in Paperless-ngx) you need to:<!--more-->

1. Add a new application set the URL as the path to exclude
2. Add a policy where the action is bypass and the selector for include is everyone

That's all there is to it!

Source: [Cloudflare Community Post](https://community.cloudflare.com/t/cloudflare-access-exclude-path-from-authentication/204893)
