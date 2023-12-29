---
title: "Copy Home Assistant Backups to Azure"
categories:
  - HomeAssistant
tags:
  - Azure
  - Backup
excerpt_separator: <!--more-->
---

As an Azure architect, I wanted to use Azure to host my Home Assistant backups but found that there weren't any add-ons or integrations that accomplished that very cleanly. A few years ago I wrote my own to solve this and it's evolved slightly since its original incarnation to use the much lighter Azcopy CLI instead of the full-blow Azure CLI and most recently a kind contributor added Service Principal authentication over my original SAS token only authentication.

## What it does

It takes the hassle out of manual backups by automating the process of copying Home Assistant snapshots to Azure. Its primary goal is to make the backup procedure seamless, ensuring that configurations and data are consistently and effortlessly backed up.

## Getting Started

If you're interested in trying out this add-on, you can find it [on GitHub](https://github.com/jak119/hassio-backup-azure-blob) or simply add it to your Home Assistant instance with [this link](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fjak119%2Fhassio-backup-azure-blob%2F)

## Feedback, bugs, and feature requests

Feedback is always welcome! Please feel free to [open an issue in the GitHub repo!](https://github.com/jak119/hassio-backup-azure-blob/issues/new)
