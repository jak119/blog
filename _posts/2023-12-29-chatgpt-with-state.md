---
title: "Sending ChatGPT Home Assistant State"
categories:
  - HomeAssistant
tags:
  - OpenAI
  - ChatGPT
excerpt_separator: <!--more-->
---

The default OpenAI / ChatGPT integration prompt only sends the API your Home Assistant instance's areas and list of devices but nothing about state. This means you could ask things about what's in a room, but not what lights are on in a room. Since I primarily wanted to do the latter I spent some time tweaking the prompt. I'm still working on tweaking it, but you can find the latest version in the Gist below. 

This template sends state information (but lacks area because it's not using devices) for lights, locks, our alarm panel, and people. It also sends some weather, location, and time information for context. Finally it asks for responses that can be spoken, this avoids the UI in Home Assistant from having some garbled text if the API sends back a list and means that you could in theory use this agent to pass along info to a TTS service.

<script src="https://gist.github.com/jak119/a34db197d3cc6886d79a3e4eb69de7c8.js"></script>
