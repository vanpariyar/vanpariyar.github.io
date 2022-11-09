---
title: "How to register dynamic Gutenberg block in WordPress ?"
slug: "how-to-register-dynamic-gutenberg-block-in-wordpress"
date: 2022-07-28T23:14:11+05:30
image : "https://user-images.githubusercontent.com/26689210/118013192-7aec9980-b36f-11eb-99b9-60facc29d930.png"
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
npx @wordpress/create-block demo-test
```

- After running command you will see that plugin is created with name `demo-test`.
- Activate `Demo Test` Plugin from the dashboard, you will see hello world block in the Post or Page Editor with :smile: emoji.

## The Change

Please check and see whole file structure in the plugin. You will find all block related code done in the `src` folder :open_file_folder:.

You will need to change the dynamic call back from the main plugin file by adding filter.





:file_folder: `src/block.json`
```javascript
{
	"$schema": "https://schemas.wp.org/trunk/block.json",
	"apiVersion": 2,
	"name": "create-block/demo-test",
	"version": "0.1.0",
	"title": "Demo Test",
	"category": "widgets",
	"icon": "smiley",
	"description": "Example static block scaffolded with Create Block tool.",
	"supports": {
		"html": false
	},
	"textdomain": "demo-test",
	"editorScript": "file:./index.js",
	"editorStyle": "file:./index.css",
	"style": "file:./style-index.css"
}

```

{{< footer-donation >}}