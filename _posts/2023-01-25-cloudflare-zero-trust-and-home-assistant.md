---
title: "Set Up Cloudflare Zero Trust and Home Assistant"
categories:
  - HomeAssistant
  - SelfHosting
tags:
  - addon
  - cloudflare
  - cloudflare teams
excerpt_separator: <!--more-->
---

If you'd like to set up and use Cloudflare Tunnels (or Cloudlfare Teams) with Home Assistant this guide should help you get started. It heavily leverages [Tobias Brenner's Cloudflared add-on](https://github.com/brenner-tobias/ha-addons).

<!--more-->

## Assumptions

- Home Assistant OS (not running standalone)
- Basic knowledge of Add Ons
- Your domain is set up on Cloudflare Zero Trust

## Get Your Tunnel Ready

1. Head to `https://dash.teams.cloudflare.com/` and log in
2. Expand Access > Tunnels
3. Click the create tunnel button
4. Give it a name (it can be anything)
5. On the connector section note the text that contains a long string of random letters and numbers **save this string for later**, this is your Cloudflare Tunnel Token
6. In the public hostname section pick your public hostname and domain
7. In the service section select `HTTP` and enter `homeassistant:8123` in the URL
8. Click save

## Set Up Home Assistant

1. [Edit your configuration.yaml](https://www.home-assistant.io/docs/configuration/#editing-configurationyaml) to inclued the following to allow Home Assistant to function behind the tunnel

   ```yaml
   http:
   use_x_forwarded_for: true
   trusted_proxies:
     - 172.30.33.0/24 # Docker network
   ```

2. Head to Add-Ons and add the repository `https://github.com/brenner-tobias/ha-addons`
   - Or use this one click URL [![Open your Home Assistant instance and show the add add-on repository dialog with a specific repository URL pre-filled.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fbrenner-tobias%2Fha-addons)
3. Install the Cloudflared add-on that's now available in your Add-On Store

   [![Open your Home Assistant instance and show the Supervisor add-on store.](https://my.home-assistant.io/badges/supervisor_store.svg)](https://my.home-assistant.io/redirect/supervisor_store/)

4. Once it's installed, head to the Add-On and the Configuration Tab

   [![Open your Home Assistant instance and show the dashboard of a Supervisor add-on.](https://my.home-assistant.io/badges/supervisor_addon.svg)](https://my.home-assistant.io/redirect/supervisor_addon/?addon=9074a9fa_cloudflared&repository_url=https%3A%2F%2Fgithub.com%2Fbrenner-tobias%2Fha-addons)

5. Enter the token you noted from step 5 above in the Cloudflare Tunnel Token box and save your configuration
6. Go back to the info tab and start the add-on
7. Monitor the log for a few entries that look like this

   ```text
   2023-01-16T21:51:07Z INF Connection f7aea022-bb92-4fa8-98f3-0cde05e55243 registered with protocol: quic connIndex=0 ip=198.41.192.27 location=BOS
   2023-01-16T21:51:08Z INF Connection 84accc1c-27d2-4e29-94fc-40a5ae2f7c3e registered with protocol: quic connIndex=1 ip=198.41.200.53 location=ORD
   ```
