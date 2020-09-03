---
title: "How to Change the Date From Custom Custom Field in Wordpress"
date: 2020-05-25T20:28:58+05:30
image : "https://user-images.githubusercontent.com/26689210/82824334-c4c24280-9ec6-11ea-97a5-8fe8f10ef66a.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["hooks", "Wordpress","filters"]
# meta description
description: "Learn how to change the date in WordPress by custom field or meta field."
# save as draft
draft: false
---

## Hi :wave:



we will use WordPress `get_the_date()` Hook.

I will explain both. If you have created meta field for date `post_custom_date`. OR using [ACF](https://wordpress.org/plugins/advanced-custom-fields/) created field with name `post_custom_date`.

## Inspiration
When I was developing the site with [Divi theme](https://www.elegantthemes.com/gallery/divi/) there is a custom post listing module but I don't want the date of publishing post instead i want my custom date which I have created with [ACF](https://wordpress.org/plugins/advanced-custom-fields/).

So I have searched and found this solution Enjoy. :tada:

Put this code in `functions.php` file.

### For custom meta Without Acf

```php

<?php
    /**
    * @here 10 is Priority and 3 is Number of arguments to be passed
    */
    add_action( 'get_the_date','custom_date_callback', 10 , 3 );
    function custom_date_callback( $the_date, $format, $post ){
        if( get_post_type() === "custom_post_type" && is_singuler("custom_post_type") ){
            $date =  sprintf( esc_html( get_post_meta('post_custom_date', $post->ID) ) );
            return $date;
        }
    }
?>

```

### For custom meta With Acf

```php

<?php
    /**
    * @here 10 is Priority and 3 is Number of arguments to be passed
    */
    add_action( 'get_the_date','custom_date_callback', 10 , 3 );
    function custom_date_callback( $the_date, $format, $post ){
        if( get_post_type() === "custom_post_type" && is_singuler("custom_post_type") ){
            $date =  sprintf( esc_html( get_field('post_custom_date', $post->ID) ) );
            return $date;
        }
    }
?>

```
checkout all hooks [hooks]({{% relref "hooks" %}})

----
## For Refrence

https://developer.wordpress.org/reference/functions/get_the_date/
https://developer.wordpress.org/reference/functions/the_date/

----
### Thank You
Thank you and canva ( For Beautiful designs ).

Thanks for the reading :+1:

#### Have any doubts or suggetions :thinking_face: 
Feel free to [connect]({{< ref "contact" >}}) social media platform given on this page :- [Contact page]({{< ref "contact" >}})


### Donate:

<a href="https://www.buymeacoffee.com/vanpariyar" rel="noopener noreferrer" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" style="height: 51px !important;width: 217px !important;" ></a>

OR [Join Buy me A Coffee](https://buymeacoff.ee/?via=vanpariyar) ( I will receive small commission by signing, You don't have to pay any money )