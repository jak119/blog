---
title: "Adaptive Lighting Component Scripts"
categories:
  - HomeAssistant
tags:
  - automation
  - adaptive lighting
---

I'm a big fan of the [Adaptive Lighting](https://github.com/basnijholt/adaptive-lighting) component and have it configured for most rooms in our house. I however find myself tweaking names, adding rooms, removing rooms, etc which meant that all the automation I had for turning on sleep mode and resetting the state (i.e., making sure it's on) kept getting stale. In came some scripts and templates!

## Sleep Mode

To find all the sleep mode switches I use this template

{% raw %}
```text
{{ states.switch | map(attribute='entity_id') | select('search',
        'switch.adaptive_lighting_sleep_mode_*') | join(',') }}
```
{% endraw %}

Then you can use that in a script (or automation) kind of like this

{% raw %}
```yaml
alias: Light Sleep Mode - Turn Off
sequence:
  - service: switch.turn_off
    data: {}
    target:
      entity_id: >
        {{ states.switch | map(attribute='entity_id') | select('search',
        'switch.adaptive_lighting_sleep_mode_*') | join(',') }}
mode: single
icon: mdi:sleep-off

```
{% endraw %}