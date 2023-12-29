---
title: "Automating Home Assistant Backup Copies to Azure"
categories:
  - HomeAssistant
tags:
  - Azure
  - Backup
excerpt_separator: <!--more-->
---

As an Azure architect, I wanted to leverage Azure to host my Home Assistant backups. However, I discovered a lack of add-ons or integrations that seamlessly accomplished this task. A few years ago, I wrote my own solution to address this issue. Over time, it has evolved, now utilizing the lighter Azcopy CLI instead of the full Azure CLI. Recently, a kind contributor enhanced it by adding Service Principal authentication alongside the original SAS token authentication.

## What it Does

This tool eliminates the manual effort involved in backups by automating the process of copying Home Assistant snapshots to Azure. Its primary goal is to make the backup procedure seamless, ensuring that configurations and data are consistently and effortlessly backed up.

## Getting Started

If you're interested in trying out this add-on, you can find it [on GitHub](https://github.com/jak119/hassio-backup-azure-blob) or simply add it to your Home Assistant instance with [this link](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fjak119%2Fhassio-backup-azure-blob%2F).

## Feedback, Bugs, and Feature Requests

Feedback is always welcome! Please feel free to [open an issue in the GitHub repo](https://github.com/jak119/hassio-backup-azure-blob/issues/new).
