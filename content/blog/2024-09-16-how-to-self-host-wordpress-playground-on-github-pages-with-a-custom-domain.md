---
title: "How to Self-Host WordPress Playground on GitHub Pages with a Custom Domain"
slug: "how-to-self-host-wordpress-playground-on-github-pages-with-a-custom-domain"
date: 2024-09-16T23:14:11+05:30
# image : "https://ia800508.us.archive.org/25/items/blog-images_202309/White%20Blue%20Illustration%20Business%20Blog%20Banner.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["Self Hosting", "WordPress Playground", "Open Source"]
# meta description
description: "In this article I have shared the solution for self host WordPress playground on the github pages and customise it"
keywords: ["WordPress Playground Selfhosting", "Github pages deployment"]
# save as draft
draft: false  
---

Hello 👋

In this post, we'll explore how to self-host a WordPress Playground on GitHub Pages. This is a fun and educational project that not only saves bandwidth for WordPress servers but also allows you to showcase your product on a custom domain.

## Why Self-Host WordPress Playground?

WordPress Playground primarily uses static files and runs directly in the user's browser. By self-hosting it on GitHub Pages, you can save bandwidth on WordPress servers and provide a unique experience by using your custom domain. This is especially useful if you want to demo your product or create a personalized WordPress Playground instance.

## How to Self-Host WordPress Playground

To get started, follow these steps:

### 1. Fork the WordPress Playground Repository

First, fork the WordPress Playground repository from [GitHub](https://github.com/WordPress/wordpress-playground). This will create a copy of the repository under your GitHub account.

### 2. Create a GitHub Actions Workflow

Next, you'll need to set up a GitHub Actions workflow to deploy the playground to GitHub Pages. Create a new workflow file, for example:

```yaml
name: Deploy to GitHub Pages

on:
  workflow_dispatch:

concurrency:
  group: website-deployment

jobs:
  build_and_deploy:
    runs-on: ubuntu-latest
    environment:
      name: playground-wordpress-net-wp-cloud
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: true
      - uses: ./.github/actions/prepare-playground
      - run: npm run build
      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          folder: dist/packages/playground/wasm-wordpress-net # The folder the action should deploy.

```

### 3. Run the Workflow Manually

After setting up the workflow, trigger it manually. This will build the project and deploy it to GitHub Pages.

## Adding a Custom Domain to GitHub Pages

To use a custom domain for your WordPress Playground, follow these steps:

1. Go to the settings of your GitHub Pages repository.
2. Under "Pages," set up your custom domain.
3. Update your domain's DNS settings:

   - **CNAME Record**: 
     - **Name**: `playground`
     - **Value**: `your-github-username.github.io`
   - **A Record**:
     - **Name**: `@` (or your domain name, e.g., `domain.com`)
     - **Value**: The IP address of GitHub Pages (check the latest IP addresses in GitHub documentation).

## Example

After completing these steps, you can have your own self-hosted playground, such as [playground.vanpariyar.in](https://playground.vanpariyar.in/).

Thanks For Reading 🙏

> This articles is rewritten from generative AI, But carefully reviewed by Me personally. Please let me know if you found any issues, in comment section below.

{{< footer-donation >}}
