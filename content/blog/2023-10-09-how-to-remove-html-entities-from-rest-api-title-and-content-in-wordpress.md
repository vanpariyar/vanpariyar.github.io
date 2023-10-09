---
title: "How to remove HTML entities from the REST API title and content in WordPress"
slug: "how-to-remove-html-entities-from-the-rest-api-title-and-content-in-wordpress"
date: 2023-10-08T23:14:11+05:30
# image : "https://ia800508.us.archive.org/25/items/blog-images_202309/White%20Blue%20Illustration%20Business%20Blog%20Banner.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["solutions", "Technology"]
tags: ["API", "WordPress"]
# meta description
description: "In this article I have shared the solution for the removing HTML entities from the WordPress REST API response"
keywords: ["WordPress REST API HTML entities", "PHP REST API HTML entity decode"]
# save as draft
draft: false  
---

Hello everyone, :wave:

## How to remove HTML entities from REST API title in WordPress

WordPress supports HTML in fields that developers wouldn't typically expect HTML in (e.g. post title). When you use the REST API to retrieve posts, the response body will include HTML, including HTML entities. This can be a problem if you are using the REST API to serve data to a non-HTML client, such as a mobile app or a JavaScript library.

To remove HTML entities from the REST API title, you can use the following code:

```php
class Customise_WordPress {

  function __construct($name) {
  // Remove the REST API HTML entities.
    $post_type = "post";
    add_filter( 'rest_prepare_ . $post_type', array( $this, 'decode_rest_api_title' ), 20, 3 );
  }
  
  /**
   * Decode HTML entities from the website title.
   *
   * @param string $response Actual response.
   * @param Object    $request Actual request.
   * @param Object    $post actual Post object.
   *
   * @return $response return text with decoded entirties.
   */
  public function decode_rest_api_title( $response, $post, $request ) {
    if ( isset( $post ) ) {
      $decoded_title = html_entity_decode( $response->data['title']['rendered'] );
      $decoded_content = html_entity_decode( $response->data['content']['rendered'] );
      $response->data['title']['rendered'] = $decoded_title;
      $response->data['content']['rendered'] = $decoded_content;
    }
    return $response;
  }
}
```

To use this code, simply copy and paste it into your theme's functions.php file. Then, create a new instance of the `Customise_WordPress` class. For example:

```php
$customise_wordpress = new Customise_WordPress('My Custom WordPress');
```

This will remove HTML entities from the REST API title for all posts.

You can also modify the code to only remove HTML entities from the REST API title for specific post types. For example, to only remove HTML entities from the REST API title for posts of the `post` type, you would change the following line:

```php
$post_type = "post";
```

to:

```php
$post_type = array('post');
```

You can also add additional filters to the `add_filter()` call to remove HTML entities from other fields in the REST API response. For example, to remove HTML entities from the REST API content, you would add the following filter:

```php
add_filter( 'rest_prepare_post_content', array( $this, 'decode_rest_api_content' ), 20, 3 );
```

The `decode_rest_api_content()` function would be similar to the `decode_rest_api_title()` function, but it would decode the `content` field instead of the `title` field.

## Benefits of removing HTML entities from the REST API title

There are several benefits to removing HTML entities from the REST API title:

* It makes the REST API response more consistent and easier to parse.
* It reduces the risk of XSS attacks.
* It improves the performance of the REST API, as HTML entities need to be decoded before they can be used.

If you are using the REST API to serve data to a non-HTML client, I recommend that you remove HTML entities from the REST API title and other fields in the REST API response.

Thanks For Reading 🙏

{{< footer-donation >}}