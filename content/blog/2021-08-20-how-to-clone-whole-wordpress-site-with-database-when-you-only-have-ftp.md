---
title: "How to Clone Whole Wordpress Site With Database When You Only Have Ftp"
date: 2021-08-20T18:18:05+05:30
image : "https://user-images.githubusercontent.com/26689210/130238376-7d9cdc20-90f7-4d73-a59f-02b9a9f14198.png"
# author
author : ["Ronak Vanpariya"] # For Example ["Ronak Vanpariya"]
# categories
categories: ["Technology", "Solutions"]
tags: ["Wordpress", "Hacks", "Adminer", "Php", "Database"]
# meta description
description: "Solution and Guide on How to Clone Whole Wordpress Site With Database When You Only Have Ftp"
keywords: ["Wordpress", "Hacks", "Adminer", "Php", "Database"]
# save as draft
draft: false
---

## Problem :thinking:
- How to Clone Whole Wordpress Site With Database When You Only Have Ftp

I came across a good idea that can save your time so I thought it would be great to share.

## What i had
I had one website's FTP only which is the WordPress website. and I was waiting to reply for 2 days.

## Output
I need to clone the whole website. in my local environment with the database installed.

## Research :book:
After searching so many articles, found a simple tool call [adminer](https://www.adminer.org/) i know many of us know and used this tool. 

## solutions :bulb:

have downloaded its PHP file. what I have done is, have uploaded that `adminer-4.1.2.php`  and renamed it to adminer.php to the document root. 

then extract credentials from the `wp-config.php` for the MYSQL.

simply hit the URL _ https://your-site/adminer.php

then entered credentials extracted from the `wp-config.php` then exported the DB from its GUI.

files I have downloaded from the FTP and Database from the adminer. that's all. 

:tada: The client replied after 2 days found he was on vacation :smile:

