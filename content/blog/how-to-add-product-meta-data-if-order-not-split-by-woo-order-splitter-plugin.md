---
title: "How to Add Product Meta Data if Order Not Split by Woo Order Splitter Plugin"
date: 2020-12-02T22:28:18+05:30

image : "https://user-images.githubusercontent.com/26689210/101244941-7ae8cd80-372f-11eb-9ef3-e17078a4db6f.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["hooks", "Wordpress", "filters"]
# meta description
description: "How to add product meta data if order not split by woo order splitter plugin."
keywords: ["Woocommerce order Splitter"]
# save as draft
draft: false
---

How to add product meta data if order not split by woo order splitter plugin
----------------------------------------------------------------------------

In this article we will learn how to add product data if order is not split.

Order split is in terms of the Multi vendor woocommerce website that have below plugin installed.

1.  [Product Vendor Plugin](https://woocommerce.com/products/product-vendors)

2.  [Woo Order Splitter](https://wordpress.org/plugins/woo-order-splitter/)

Firstly Let me give the idea about both Plugins.

The Product vendor plugin is Creating multi vendor marketplace that have multiple vendors like [amazon](http://amazon.in/) we have multiple sellers that sell their limited Product.

But amazon has multiple products like TV, Fridge , mobile, Mitti Pot, Footwear and lots of variety. Because all sellers can not have all things ya there are some exceptions Like Cloudtail and all.but small sellers have limited items to sell.

So if anybody wants to make a website like amazon multi seller feature then this website is the right place for you.

Let's Now understand the What the Order splitter is doing.It is very interesting to see here. We can split order on any term, which means if we want to split order by order vendor again taking the example of Amazon ( not sponsored :-) ).

If we order one Grocery item and one electronic item like a Bag of Rice and Apple Iphone then there is a sure probability that our order has multiple sellers. So by default woocommerce does not assign vendors and split the order on the Product based vendor but this plugin does.

Let's assume we have a woocommerce site and have thousands of products and hundreds of vendors then it will be very hard and time consuming to assign and maintain orders and deliveries with communication with different sellers.

We can use this plugin in this scenario, this plugin is easily splitting order, in The depth this plugin finds the vendor of each product, then makes the list of products in the order for particular seller. After that it creates a new order and assigns the vendor to specific order then the vendor can see on their dashboard and Fulfillment of the Order process starts.

Now you will be wondering what happens to my original order ? yes that order is definitely going to trash and the user profile will show the Two order if my original order id is 3366 then 3366 order will be deleted and new order created with the order id 3367 and 3368. And both will assign to their sellers.

We can add below code if user Order not split but want to assign order vendor to the user order.
```php
<?php
/**
* Customization for Order meta
*
*/

add_action('woocommerce_thankyou', 'add_custom_order_meta', 10, 1);

functionadd_custom_order_meta( $order_id ) {

    $order = wc_get_order($order_id);

    /**
    * if Order splitter works the order will be trash and empty array will return.
    * so we are checking the order content.
    */
    if( ! empty( $order ) ){

    $items = $order->get_items();

        foreach( $items as $key=> $item ){
            $product_id = $item->get_product_id();
            $vendor = get_the_terms( $product_id, 'wcpv_product_vendors' );
            $vendor_id = $vendor[0]->term_id;
            update_post_meta($order_id, '_vendor_id', $vendor_id);

            $vendor_data = get_term_meta($vendor_id, 'vendor_data');
            $vendor_info = array(
                'vendor_email' => $vendor_data[0]['email'],
                'vendor_name' => $vendor[0]->name,
                'vendor_slug' => $vendor[0]->slug,
            );

            update_post_meta($order_id, 'wos_vendor_data', $vendor_info);

            break;

            // For test uncomment this and place order one in view source.

            // print_r( get_post_meta($order_id, 'wos_vendor_data', true) );

            // die();

        }

    }

}
```

{{< footer-donation >}}