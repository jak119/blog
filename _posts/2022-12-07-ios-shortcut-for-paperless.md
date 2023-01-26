---
title: "Creating an iOS Shortcut for Paperless"
categories:
  - SelfHosting
tags:
  - paperless
  - ios shortcuts
---

Over the past couple of years I've slowly been putting all of my paperwork into Paperless (first Paperless-ng and now [Paperless-ngx](https://github.com/paperless-ngx/paperless-ngx#readme)). One of the things I've been meaning to do for a while now is create an [iOS Shortcut](https://support.apple.com/guide/shortcuts/welcome/ios) to directly upload a file to Paperless without needing to email it or use the not-so-great mobile web interface. This means I could open a PDF someone sends me in iMessage and upload it straight to Paperless without any intermediary step of saving it to iCloud or emailing it.

## POST to Paperless

I'll skip to the interesting part, below is a screenshot that shows most of what you need to configure in order to `POST` directly to Paperless

![Screenshot of iOS Shortcuts](/assets/img/paperless_upload_action.jpeg)

You'll use the "Get contents of" action and the URL will be `$yourURL` and the API URL is `/api/documents/post_document/` (including the trailing slash).

The method is `POST` and you'll need to pass an authorization header. In my case I chose to [create a token](#creating-an-auth-token) and provide it prefixed with `Token`.

The key part of the body is to select the form type and provide a `document` which in my case is `Shortcut Input`.

If `Shortcut Input` doesn't appear as an option hit the little _i_ icon at the bottom of the screen and turn on "Show in Share Sheet" then go back to your shortcut.

In my example you may also notice I provided a few extra form fields which are nicely documented in [the API docs](https://docs.paperless-ngx.com/api/#file-uploads). I show a couple of inputs, save the input to a variable, and then pass that variable in here.

## Creating an Auth Token

1. Go to your Paperless instance
1. Log in as an admin
1. Go to the admin panel (/admin or scroll down on the left)
1. Click tokens
1. Click add token
1. Select add a user to associate the token to (it may be a good idea to create a non-admin user for this)
1. Click save
1. Copy your new token

## Using this Shortcut with Cloudflare Access / Tunnels

In my case I needed to solve not only for talking to Paperless, but also authenticating to Cloudflare Zero Trust which was relatively straightforward once I pieced together a few docs. I put together [this post on Cloudflare Zero Trust Service Auth]({% post_url 2022-12-07-cloudflare-service-auth %}) for reference.
