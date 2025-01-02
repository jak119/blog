---
title: "Using OpenAI / ChatGPT and Home Assistant to Generate a Morning Summary (as of December 2023)"
categories:
  - HomeAssistant
tags:
  - OpenAI
  - ChatGPT
excerpt_separator: <!--more-->
---

I'm a little late jumping on the OpenAI / ChatGPT bandwagon, but I decided to try out [Allen Porter's seemingly infamous blueprint](https://gist.github.com/allenporter/e70d9eb090c7dbdd593cf526e07b4abe). However, many of the OpenAI blog posts I found were a bit out of date. Below is how I set it up.

## Get an OpenAI API Key

1. First, create an [OpenAI account or sign in](https://platform.openai.com/). Next, navigate to the [API key page](https://platform.openai.com/account/api-keys) and "Create new secret key". Make sure to save this somewhere safe and do not share it with anyone.
2. Fund your account from the [Billing page](https://platform.openai.com/account/billing/overview).

That's it. As of the time of writing, it seems that OpenAI no longer grants a buck of credit to get started (or at least mine expired), so I did have to fund my account with a minimum of $5 to get started in earnest. I did have some free credit, but it expired before I actually got around to setting this up.

## Set up OpenAI in Home Assistant

### Add the OpenAI Integration

1. Add the [OpenAI Integration](https://my.home-assistant.io/redirect/config_flow_start/?domain=openai_conversation) and paste your API key from above.

You can stop here, but to avoid sending unnecessary data to OpenAI, I also did the following:

2. Navigate to the OpenAI integration from the [integrations dashboard](https://my.home-assistant.io/redirect/integrations/).
3. Click configure and cleared out the prompt template.

   Note: I was having issues with this, but found that I could just insert a simple space then save.

4. You can also change the model that's being used here; I left it on `gpt-3.5-turbo`. You can find a [full list of models in the OpenAI Platform docs](https://platform.openai.com/docs/models).

   I did try GPT-4 but found that it was about 5x more expensive (costing ~$0.04 per call), and I wanted to be frugal with 3.5, which is running me <$0.01 / day.

### Add a voice assistant

1. In Home Assistant, head to Settings > Voice Assistants or use [this link](https://my.home-assistant.io/redirect/voice_assistants/).
2. Click the Add Assistant button.
3. Give it a name; for conversation agent, select the OpenAI integration you added above, tweak the other settings if you want, and click create.

### Ensure you have data in Home Assistant

The Blueprint linked at the top of this post assumes you have a working weather integration, your calendar available, and a notify service that supports enough long messages. For me, this meant using:

- [Google Calendar](https://www.home-assistant.io/integrations/google/)
- The [US National Weather Service (NWS)](https://www.home-assistant.io/integrations/nws/)
- [SendGrid](https://www.home-assistant.io/integrations/sendgrid/)

### Import the Blueprint

I started off by using Allen Porter's blueprint, which you can import easily using [this link](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.github.com%2Fallenporter%2Fe70d9eb090c7dbdd593cf526e07b4abe) and follow the prompts.

Reading through the comments on the Gist, I noticed [this comment](https://gist.github.com/allenporter/e70d9eb090c7dbdd593cf526e07b4abe?permalink_comment_id=4796049#gistcomment-4796049) that addressed one of my big needs, which was to feed multiple calendars.

To make importing (for others) easier, I've gone ahead and hosted the version found in the comment as [a Gist](https://gist.github.com/jak119/0abf5489a67c364311490785be974a6e) so that it can be [easily imported](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.github.com%2Fjak119%2F0abf5489a67c364311490785be974a6e).

## Some "Gotchas"

- I noticed that responses were getting truncated, and I read somewhere that I needed to increase the max "tokens" configured in the OpenAI integration.

## Enhancements I'd like to add

- My work calendar isn't available to Home Assistant, so I'd like to add a hint (probably using the [Workday integration](https://www.home-assistant.io/integrations/workday/)) on whether it's a workday so that can be worked into the response.
- Adding some logic to handle traveling or sharing in the prompt if I'm home or not.
