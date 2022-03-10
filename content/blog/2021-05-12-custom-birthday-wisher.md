---
title: "Make your own Custom Birthday Wisher"
date: 2021-03-28T23:14:11+05:30
image : "https://user-images.githubusercontent.com/26689210/118013192-7aec9980-b36f-11eb-99b9-60facc29d930.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["tools", "birthday", "javascript"]
# meta description
description: "Make your own Custom Birthday Wisher with javascript no database required to run this tool"  
keywords: ["Birthday Wisher Tool", "Best tool to wishes for birthday", "Creative way to wish birthday"]
# save as draft
draft: false
---

### Introduction
:wave: Hello friend, :scroll: :slightly_smiling_face: :house:		

I was looking for a very creative way to wish someone *" Happy Birthday "* :tada: . As you think we will make some creativity using javascript. also added this to the List of [Tools]({{< ref "page/tools" >}} "tools")

> All Code Given Here:-  [Github Link](https://github.com/vanpariyar/birthday-wishes/ "birthday Wishes Tool")

> Live demo Here:-  [Live Demo](https://vanpariyar.github.io/birthday-wishes/?name=ShreeHariJI "birthday Wishes Tool Live Demo")


### Template
You can found this HTML template on anywhere, Websites like codepen. I have taken from codepen.

__*ProTip:*__ select very simple first time for learning :hand:

i have chosed once very simple template. i have mentioned in the code. <a target="_blank" href="https://github.com/vanpariyar/birthday-wishes/blob/main/index.html">My Template Link</a>

### How to make tool dynamic
If the birthday wishes tool is dynamic then we do not need to make changes every time, so we can send personalized emails from the link like this.

![demo of personal birthday wishes tool](https://i.imgur.com/U855XJT.png)

if you see we have one attribute `?name` in the URL. That is the key to make this dynamic :blush:

`https://vanpariyar.github.io/birthday-wishes/?name=ShreeHariJI`

- this is our HTML
```html
<div class="text">
    <h1>Happy Birthday! <span id="name">To you!!!</span> </h1>
    <p>I hope you have a wonderful birthday</p>
    <p class="muted">- Enjoy Birthday</p>
</div>
```

we will replave with `<span id="name">To you!!!</span>` by javascript.

- Add JavaScript

```javascript
var parseQueryString = function() {

    var str = window.location.search;
    var objURL = {};

    str.replace(
        new RegExp( "([^?=&]+)(=([^&]*))?", "g" ),
        function( $0, $1, $2, $3 ){
            objURL[ $1 ] = $3;
        }
    );
    return objURL;
};

//Example how to use it: 
var params = parseQueryString(); 

document.getElementById('name').innerText = ( params.name ) ? decodeURIComponent(params.name) : 'To You'; 
```

### Finishing Up

You can host this tool anywhere you want to host. I  prefer Github pages. But you can host anywhere like netlify, varcel, Heroku etc...

### How to use

Add parameter to the end of the URL like

`https://vanpariyar.github.io/birthday-wishes/?name=ShreeHariJI`

> Here `?name=ShreeHariJI` is parameter

change with you name and copy to browser you will see your desired name


{{< footer-donation >}}