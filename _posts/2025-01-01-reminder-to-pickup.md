---
title: "Using Home Assistant to Monitor Travel Time"
categories:
  - HomeAssistant
tags:
  - reminder
  - notifications
excerpt_separator: <!--more-->
toc: false
---

Today I'm sharing how I set up an automation to remind me when it's time to pick up my wife. This uses a combination of a datetime helper, the Waze integration, a template helper, and automations.

## What This Is Comprised Of

1. **Datetime Helper**: Allows you to set the time when you need to pick someone up.
2. **Waze Integration**: Calculates travel time between two locations using `person` entities.
3. **Template Helper**: Dynamically calculates when to leave based on travel time and pickup time.
4. **Push Notification**: Sends an alert to your phone when it's time to leave using a `notify` service.

## Getting Started

### Step 1: Create a Datetime Helper

In Home Assistant, go to [Settings \> Devices \& Services \> Helpers](https://my.home-assistant.io/redirect/helpers/) and create a datetime helper. Name it something like `pickup_time` which will become `input_datetime.pickup_time`.

### Step 2: Configure the Waze Integration

[Add the Waze Travel Time integration](https://my.home-assistant.io/redirect/config_flow_start?domain=waze_travel_time) to Home Assistant with the origin as `person.you` and destination as `person.otherperson`. This integration will calculate the travel time between your current location and another person.

### Step 3: Create a Template Sensor

Create a new template sensor, this template sensor calculates the time to leave based on the datetime helper and the Waze travel time. Let's assume it'll be named `sensor.time_to_leave`.

{% raw %}
```text
{% set travel_time = states('sensor.waze_travel_time') | int(default=0) %}
{% set pickup_time = (states('input_datetime.pickup_time') | as_datetime | default(now())).replace(tzinfo=now().tzinfo) %}
{% if pickup_time > now() %}
  {{ (pickup_time - timedelta(minutes=travel_time)) | as_timestamp | timestamp_local }}
{% else %}
  {{ null }}
{% endif %}
```
{% endraw %}

### Step 4: Write the Automation

This automation sends a push notification to your phone when it's time to leave.

```yaml
alias: Reminder to leave to pickup ...
description: ""
triggers:
  - trigger: time
    at: sensor.time_to_leave
    id: now
  - trigger: time
    at:
      entity_id: sensor.time_to_leave
      offset: "-00:05:00"
conditions: []
actions:
  - if:
      - condition: template
        value_template: "{{trigger.id == 'now' }}"
    then:
      - action: notify.mobile_app_iphone
        metadata: {}
        data:
          message: Go via {{state_attr('sensor.waze_travel_time','route') }}
          title: Leave now!
    else:
      - action: notify.mobile_app_iphone
        metadata: {}
        data:
          message: Go via {{state_attr('sensor.waze_travel_time','route') }}
          title: >-
            Leave in {{ states('sensor.time_to_leave') | as_datetime |
            time_until }}
mode: single
```
