---
title: "How to Add Anything After Wordpress Title in Backend ?"
date: 2020-07-29T22:03:57+05:30
image : "https://user-images.githubusercontent.com/26689210/100902103-93b47180-34ea-11eb-9240-49bf5984c1e5.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["hooks", "Wordpress", "filters"]
# meta description
description: "Learn how to add any Html / Text after wordpress editor title field."
# save as draft
draft: false
---

hi :wave: Learn how to add any Html / Text after wordpress editor title field.

> Note: This is only for the Classic Editor i am not sure about Gutenberg/Block Editor. 

Actually you will learn about how  


- [x] How to add title in Classis editor
- [ ] How to add in Gutenberg Editor

Add this in your `function.php` file

> Here our post type is **Tags**.

```php
<?php
add_action( 'edit_form_before_permalink' , 'add_text_below_tag_post_title' );
function add_text_below_tag_post_title( ){
    global $post;
    if ( get_post_type($post) === 'tags' ){
        echo "<span style='color: red'>demo alert (THis is the red text)</span>";
    }
}
?>
```
---

Thanks for the reading :+1:

#### Have any doubts or suggetions :thinking_face: 
Feel free to [connect]({{< ref "contact" >}}) social media platform given on this page :- [Contact page]({{< ref "contact" >}})

<a href="https://www.buymeacoffee.com/vanpariyar" rel="noopener noreferrer" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" style="height: 51px !important;width: 217px !important;" ></a>

OR

[Join Buy me A Coffee](https://buymeacoff.ee/?via=vanpariyar) ( I will receive small commission by signing, You don,t have to pay any money )
