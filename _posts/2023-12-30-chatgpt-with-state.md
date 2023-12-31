---
title: "Sending ChatGPT Home Assistant State"
categories:
  - HomeAssistant
tags:
  - OpenAI
  - ChatGPT
excerpt_separator: <!--more-->
---

The default OpenAI / ChatGPT integration prompt only sends the API your Home Assistant instance's areas and list of devices, but it doesn't include the state information. This means that you could ask questions about what's in a room, but not about which lights are on in a room. Since my primary goal was to inquire about the lights, I spent some time tweaking the prompt.<!--more--> Although I'm still working on it, you can find the latest version in the Gist below.

This template includes state information for lights, locks, our alarm panel, and people (excluding area information as it isn't using devices). Additionally, it provides weather, location, and time information for context. Furthermore, it requests responses that can be spoken, which prevents the UI in Home Assistant from displaying garbled text in case the API sends back a list. This also means that you can potentially use this agent to pass along information to a Text-to-Speech (TTS) service.

<script src="https://gist.github.com/jak119/a34db197d3cc6886d79a3e4eb69de7c8.js"></script>
