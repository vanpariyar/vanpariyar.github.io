---
title: "How to Automate the Wordpress Plugin Upload With Github Actions ?"
date: 2020-07-03T22:13:29+05:30
image : "https://user-images.githubusercontent.com/26689210/86487296-5604be80-bd7b-11ea-91a3-d6f192a32369.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["snippets", "Wordpress","github","automation"]
# meta description
description: "learn to Automate the Wordpress Plugin Upload With Github Actions to svn repository."
# save as draft
draft: false
---

Hello Friends, :wave:
today we will learn about something interesting which is automation for wordoress svn repository.

```javascript
Automation is fun and make us more productive.
```
## Introduction
I recommand you to open side by side this github link <a href="https://github.com/vanpariyar/wp-post-views" target="_blank">Plugin Repo</a> to understand properly.

> First of all we need atleast one plugin hosted in the Wordpress Plugin directory.

## Get started
- Upload Your plugin to github

- after uplaoding your plugin 

goto `actions > setup new workflow yourself`

![setup new workflow in github](https://user-images.githubusercontent.com/26689210/86532198-9c762c80-bee5-11ea-8cc4-c2103ec0da5a.png)

<a href="https://github.com/vanpariyar/wp-post-views/blob/master/.github/workflows/main.yml" rel="nofollow">Click To Copy Workflow File</a> and paste on your File.

change the plugin url and other stuff that you want to ingnore.Like i have ingnored readme.md etc.

## Creating Secrets on Github

For Doing That goto settings of Repository.

Click on Secret Tab.

![Screenshot from 2020-07-05 17-50-31](https://user-images.githubusercontent.com/26689210/86532526-5e2e3c80-bee8-11ea-85b9-a707340cfb02.png)

Then add New As mentions in the Workflow file.
```javascript
WORDPRESS_PASSWORD

WORDPRESS_USERNAME
```
By doing this setup done.

## How to upload on wordpress

As mentions on Workflow file we will run this setup on every tag release.

```shell
name: Deploy
on:
  push:
    tags:
      - '*'
jobs:
  tag:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: WordPress Plugin Deploy
      #see rtCamp  repo for the 
      uses: rtCamp/action-wordpress-org-plugin-deploy@master
      env:
        #CUSTOM_COMMAND: ''
        #CUSTOM_PATH: ''
        EXCLUDE_LIST: docker-compose.yml README.md _config.yml
        SLUG: wp-post-views
        WORDPRESS_PASSWORD: ${{ secrets.WORDPRESS_PASSWORD }}
        WORDPRESS_USERNAME: ${{ secrets.WORDPRESS_USERNAME }}
```

To release tag Goto your Release Then  ` Click Draft a new Release.`

when you create new relese do not forgot to change your plugin version and readme.txt file version


{{< footer-donation >}}
