---
title: "How to Remove Divi Shortcodes From Content ?"
slug: "how-to-remove-divi-shortcodes-from-content"
date: 2022-01-18T22:22:16+05:30
image : "https://user-images.githubusercontent.com/26689210/149984688-43fee914-acbc-4165-8190-d9275bc9cf3e.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["divi", "shortcode", "tips"]
# meta description
description: "[SOLVED]How to Remove Divi Shortcodes From Content"
keywords: ["remove divi shortcode", "remove shortcode from content"]
# save as draft
draft: false
---

Hello Friends as You know we are learning everyday in our life. so today we will learn how to remove shortcodes from the content while migrating our site.

## Problem with Content

when i was migrating the website we got the lots of the divi shortcodes in the content.

when i was researching the solution but i ended up with the plugin that is paid. so me and my colleague decided to solve with PHP script.



### This code can be use to Remove Divi shortcodes from the wordpress blogs and Content

put this code in the `fucntions.php` file

```php
global $wpdb;
$allPosts = $wpdb->get_results("SELECT * FROM `wp_posts`");
foreach($allPosts as $post){
  $content = RemoveShortcodes('/\[\/?et_pb.*?\]/', '', $post->post_content);
  $wpdb->update(
    'wp_posts',array('post_content' => $content),array( 'ID' => $post->ID )
  );
}

function RemoveShortcodes($beginning, $end, $string) {
  $beginningPos = strpos($string, $beginning);
  $endPos = strpos($string, $end);
  if ($beginningPos === false || $endPos === false) {return $string;}
  $textToDelete = substr($string, $beginningPos, ($endPos + strlen($end)) - $beginningPos);
  return RemoveShortcodes($beginning, $end, str_replace($textToDelete, '', $string));
}
```

code credit : https://github.com/vidursingh96

{{< footer-donation >}}