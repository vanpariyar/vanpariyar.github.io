---
title: "How Create NPM Package With Scoped @organization"
date: 2021-06-11T16:43:52+05:30
image : "https://user-images.githubusercontent.com/26689210/122342638-803a9680-cf62-11eb-830d-6d18ff16d4f9.png"
# author
author : ["Ronak Vanpariya"] # For Example ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["Package", "NPM", "Javascript"]
# meta description
description: "Create Npm Package With Scoped @organization with step by step instruction"
keywords: ["npm package", "scoped NPM package"]
# save as draft
draft: false
---


## Introduction
Today we will learn how to create a NPM package like this https://www.npmjs.com/package/@vanpariyar/text-manipulation

I was wondering how I can make my own package in the javascript and publish it to the NPM registry ? :thinking:.

So I found the below step that you can easily register your NPM package with your scoped. :diya_lamp: ( This is Lamp in India :bulb: :smile:) 
Like if you see `@angular/package-name`

## Requirements :100:
- Node.js installed
- git installed
- NPM account for publishing package.

## Starting
Let's start the development now.

```shell
mkdir text-manipulation
cd text-manipulation
Npm login
```
After `npm login`  enter your username, password, email


```shell
npm init --scope=@my-org 
// OR
 npm init --scope=@my-username
```
Now you will have the prompt that you need to answer for your package. Like the Package version, Github Repo etc.

Now `open index.js` in your preferred editor. Then write your code in the file. :pen:

Add `.gitignore` to ignore `node_modules`

```shell
# .gitignore

node_mudules

```

Then if you have a public account you need to add this parameter with the `npm publish` command.

```shell
npm publish --access public
```

## Conclusion 
Nice, :tada: You have published your first NPM package.

{{< footer-donation >}}