---
title: Deploy your Astro Site with Cleavr
description: How to deploy your Astro site to your VPS server using Cleavr.
layout: ~/layouts/DeployGuideLayout.astro
i18nReady: true
---

You can deploy your Astro project to your own Virtual Private Server (VPS) using [Cleavr](https://cleavr.io/), a server and app deployment management tool.

:::tip
Check out [the Astro guide in Cleavr's docs](https://docs.cleavr.io/guides/astro)!
:::

## Prerequisites 

To get started, you will need:

- A Cleavr account
- A server on your VPS provider using Cleavr

## Add your site

1. In Cleavr, navigate to the server you want to add your Astro project to.

2. Select **Add Site** and fill in the details for your application, such as domain name.

3. For **App Type**, select 'NodeJS Static' or 'NodeJS SSR' according to how you are setting up your Astro app.
   
4. For Static apps, set **Artifact Folder** to `dist`.
   
5. For SSR apps:
   - Set **Entry Point** to `entry.mjs`.
   - Set **Artifact Folder** to `dist/server`.
   
6. Select **Add** to add the site to your server.


## Setup and deploy

1. Once your new site is added, click **Setup and deploy**.
   
2. Select the **VC Profile**, **Repo**, and **Branch** for your Astro Project.
   
3. Make any additional configurations neccesary for your project.
   
4. Click on the **Deployments** tab and then click on **Deploy**.

Congratulations, you've just deployed your Astro app!