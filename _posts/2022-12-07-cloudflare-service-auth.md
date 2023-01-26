---
title: "How to Use Service Auth on Cloudflare Access"
categories:
  - SelfHosting
tags:
  - service auth
  - cloudflare teams
  - cloudflare
---

I didn't love Cloudflare's documentation, so here's a (very) quick guide to using Service Auth on Cloudflare Access. This guide assumes you've gone through and [set up Cloudflare Zero Trust](https://developers.cloudflare.com/cloudflare-one/setup/) and have an existing application.

## Create a Token

1. Head to your [dashboard](https://one.dash.cloudflare.com/)
1. Expand Access > Service Auth
1. Create a service token by clicking the create service token button and save the generated headers and values in a safe place

## Add a Policy

1. Expand Access > Applications
1. Click Edit on the application you want to use the service token for
1. Add a **new** policy
   - You can't add a service token to a policy that has users
1. Give your policy a name, **under action select service auth**
1. Add an include rule
   1. Select Service Token and add the token you created above
1. Save your new policy

## Using Tokens

In your request header be sure to include `CF-Access-Client-Id` and `CF-Access-Client-Secret` as headers.
