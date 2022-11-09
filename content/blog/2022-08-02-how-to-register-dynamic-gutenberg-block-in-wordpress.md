---
title: "How to register dynamic Gutenberg block in WordPress ?"
slug: "how-to-register-dynamic-gutenberg-block-in-wordpress"
date: 2022-07-28T23:14:11+05:30
image : "https://user-images.githubusercontent.com/26689210/200741064-dbc5af12-37a7-492a-b2e3-3e77076ad9bb.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["WordPress", "Snippets", "Javascript", "PHP"]
# meta description
description: "This tutorial will show how to register dynamic Gutenberg block in WordPress"  
keywords: ["Dynamic Gutenberg Block", "Change Existing Block Render Callback", "Learn Gutenberg"]
# save as draft
draft: false
---

## Introduction
:wave: Hello friend, :scroll: :slightly_smiling_face: :house:		

I was working on Gutenberg Side from a large amount of time. :timer_clock:. If you comfortable with the WordPress development blog you can ues the docs itself :point_right: [Official Handbook](https://developer.wordpress.org/block-editor/ "Wordpress Block Editor Handbook"). 

In this tutorial you will learn how to make [dynamic block](https://developer.wordpress.org/block-editor/how-to-guides/block-tutorial/creating-dynamic-blocks/) using Gutenberg.

## Setup
- Any local development system with node.js and NPM/Yarn installed.
- Run command in plugin folder's via terminal 

```bash
$ npx @wordpress/create-block demo-test --variant dynamic
```

:smile: That's it all setup is done now.

- After running command you will see that plugin is created with name `demo-test`.
- Activate `Demo Test` Plugin from the dashboard, you will see hello world block in the Post or Page Editor with :smile: emoji.

## The Change

Please check and see whole file structure in the plugin. You will find all block related code done in the `src` folder :open_file_folder:.

Now You will not need to change the dynamic call back from the main plugin file by adding filter.

You can start code in `edit.js`.

in `src` folder you will see `template.php` which is preconfigured by command.

You can write your code in the tempate and see more here :point_right: [Official NPM Package](https://www.npmjs.com/package/@wordpress/create-block/ "WordPress Create Block NPM package").

{{< footer-donation >}}