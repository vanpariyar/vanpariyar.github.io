---
title: "How to Get an Array of Random Numbers or elements in Wordpress ?"
date: 2020-06-30T09:51:14+05:30
image : "https://user-images.githubusercontent.com/26689210/86144953-f8bb0400-bb13-11ea-81a7-929eb9232a1c.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["snippets", "Wordpress","php"]
# meta description
description: "learn to Get an Array of Random Numbers or elements in Wordpress."
# save as draft
draft: false
---

In this blog post, we will discuss generating a different type of array of numbers.

### Topics:
- How to generate a random number.
- How to generate random indexes from the array.
- How to generate random elements from the array.

Hi :wave: Welcome

---

### How to generate a Random number.

we will use this function in the below code.

```php
<?php
function get_random_element( $array_of_element ){
    return mt_rand(0, count($array_of_element) - 1);
}
?>
```
----

### How to generate random indexes from the array.
- we have used this code to loop the above-mentioned function.

```php {linenos=false,hl_lines=[5],linenostart=1}
<?php
function get_random_array( $array_of_element, $count_return ){
    $random_array = array();
    while( count( $random_array ) <  $count_return){
        $random_number = get_random_element( $array_of_element );
        if( ! in_array( $random_number , $random_array ) ){
            array_push( $random_array, $random_number );
        }
    }
    return $random_array;
}
?>
```
---

### How to generate random elements from the array.
In this function, we have used the above function the same to get random indexes from the array.

```php {linenos=false,hl_lines=[3],linenostart=1}
<?php
function get_random_values( $array_of_element, $count_return = 3 ){
    $random_index = get_random_array( $array_of_element, $count_return );
    $return_array = array();
    foreach( $random_index as $key => $random_index_number ){
        $return_array[$key] = $array_of_element[$random_index_number];
    }
    return $return_array;
}
?>
```

---

### Protip

- You can combine this code like this and get the array of values by passing an array.

```php {linenos=false,hl_lines=[3,10,19],linenostart=1}
<?php

function get_random_element( $array_of_element ){
    return mt_rand(0, count($array_of_element) - 1);
}

function get_random_array( $array_of_element, $count_return ){
    $random_array = array();
    while( count( $random_array ) <  $count_return){
        $random_number = get_random_element( $array_of_element );
        if( ! in_array( $random_number , $random_array ) ){
            array_push( $random_array, $random_number );
        }
    }
    return $random_array;
}

function get_random_values( $array_of_element, $count_return = 3 ){
    $random_index = get_random_array( $array_of_element, $count_return );
    $return_array = array();
    foreach( $random_index as $key => $random_index_number ){
        $return_array[$key] = $array_of_element[$random_index_number];
    }
    return $return_array;
}
?>
```

---

### conclution 

- You can call this function like:

```php {linenos=false,hl_lines=[3],linenostart=1}
<?php

$large_array = array( 10, 25, 85, 47, 78, 89, 79, 258, 74, 2 );

/**
 * $arg-1 is array of elements , 
 * $arg-2 is number of elements to be return
*/
$random_array = get_random_values( $large_array, 4 );

?>
```

{{< footer-donation >}}