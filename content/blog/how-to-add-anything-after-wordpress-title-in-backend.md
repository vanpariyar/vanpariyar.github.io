---
title: "How to Add Anything After Wordpress Title in Backend ?"
date: 2020-07-29T22:03:57+05:30
image : "https://user-images.githubusercontent.com/26689210/81397515-1b005900-9145-11ea-9612-6848c459dbcf.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["Google", "Wordpress"]
# meta description
description: "Learn how to add any Html / Text after wordpress editor title field."
# save as draft
draft: true
---

hi :wave: Learn how to add any Html / Text after wordpress editor title field.

> Note: This is the new 

Actually you will learn about how  


- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

```php
<?php
add_action( 'edit_form_before_permalink' , 'add_text_below_tag_post_title' );
function add_text_below_tag_post_title( ){
    global $post;
    if ( get_post_type($post) === 'tags' ){
        echo "<span style='color: red'>Auto-tag (choose carefully, will be linked in every piece)</span>";
    }
}
?>
```
