---
title: "How to Change Page Title by Custom Field in Wordpress"
date: 2020-05-22T11:58:48+05:30
image : "https://user-images.githubusercontent.com/26689210/82638777-28c5dc00-9c25-11ea-9a9f-bdac018858f7.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["hooks", "Wordpress"]
# meta description
description: "Learn how to change the page title in WordPress by custom field or meta field."
# save as draft
draft: false
---

## Prerequisite

If I get right you come here to change this :blush: see in Pic below.

![How to Change Page Title by Custom Field in Wordpress](https://user-images.githubusercontent.com/26689210/82746322-014d4b80-9dac-11ea-850c-e9c085ced98f.png)

----

If you are using **custom theme** make sure you have used this hook in your head tag. Because we are going to **filter that value** based on ` wp_title( ); ` hook.

```php
   <title>
        <?php wp_title( '|', true, 'right' ); ?>
    </title> 
```

Let's say we have custom field meta key `_custom_post_name`.

If you have created the [ACF](https://www.advancedcustomfields.com/) field then your field name will be "_" + `your_field_name` means if you have created `page_title` then your meta key will be `_page_title`. :thumbsup:

## how to modify title?

- For any single Page or Post

```php
<?php
/**
 * Customize the title for the Single page, if one is not set.
 *
 * @param string $title The original title.
 * @return string The title to use.
 */

add_filter( 'wp_title', 'change_page_title_callabck', 10 , 2 );

function change_page_title_callabck( $title , $separator)
{
    /**
    * To change the title on your single or post page
    */
    if( is_single() ){ 
        // Add your meta key here
        $custom_post_title = get_post_meta( get_the_ID(),'add_your_meta_key', true);
        if( $custom_post_title ){
            $title = $custom_post_title ." ".$seprator." ";
        }
        
    }
    return $title;
    
}
?>
```

- For custom post type

```php
<?php
/**
 * Customize the title for the Single page, if one is not set.
 *
 * @param string $title The original title.
 * @return string The title to use.
 */

add_filter( 'wp_title', 'change_page_title_callabck', 10 , 2 );

function change_page_title_callabck( $title , $separator)
{
    /**
    * To change the title on your single or post page
    */
    if( is_single() && 'custom_post_type' == get_post_type() ){ 
        // Add your meta key here
        $custom_post_title = get_post_meta( get_the_ID(),'add_your_meta_key', true);
        if( $custom_post_title ){
            $title = $custom_post_title ." ".$seprator." ";
        }
        
    }
    return $title;
    
}
?>
```

----

## For different Pages?

- for category you can use `is_cat()` OR `is_tax()`.
- for archive you can use `is_archive()`.

----

for  Reference of ` wp_title( ); ` hook.

https://developer.wordpress.org/reference/hooks/wp_title/

https://developer.wordpress.org/reference/functions/wp_title/

{{< footer-donation >}}