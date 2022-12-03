---
title: "Using Events for Holiday or Temporary Automation"
categories:
  - HomeAssistant
tags:
  - events
  - automation
---

One of the big things I do with Home Assistant is call scripts via Google Assistant. We use a "goodnight" routine in Google Home that fires a script in Home Assistant (scripts are surfaced as scenes in Google Home). This runs a bunch of routine actions like turning off a group of lights, arming our alarm, and locking our doors.

With the holiday season upon us I also wanted to add in turning off our Christmas lights, but didn't want to add them into the regular script since I'd inevitably forget to remove them and it'd start erroring out.

To save future me some troubleshooting, I instead added an action that looks like this

```yaml
event: goodnight_script
event_data: {}
```

so that I can write individual automations with a simple trigger based on the `goodnight_script` event. I can add, remove, and disable them without overthinking what other implications there may be. And when I innevitably forget to disable an automation and remove the plug from Home Assistant, only one automation will fail and it won't cascade or prevent further steps in one giant automation from running.
