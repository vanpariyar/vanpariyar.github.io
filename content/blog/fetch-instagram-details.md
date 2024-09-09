---
title: "Fetch Instagram Details"
date: 2024-09-09T10:00:00+05:30
draft: false
image : "https://user-images.githubusercontent.com/26689210/81502620-9f490c80-92fc-11ea-8775-43e099db29a8.png"

# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["Instagram", "API", "Wordpress"]
# meta description
description: "How to fetch Instagram details using the latest API requirements."

---

> This guide has been updated: Instagram now requires an access token to fetch user data. This guide covers how to authenticate and retrieve user details using the Instagram Graph API.

## Get-Instagram-Details (Updated)

Instagram has deprecated its public API, and now you need an **Instagram Access Token** to fetch user data. To retrieve details like username, profile picture, bio, and follower count, you must authenticate your app and get the appropriate permissions using the Instagram Graph API.

### Steps to Get Instagram Details

1. **Set up your Instagram Developer account:**
   - Go to the [Instagram for Developers](https://developers.facebook.com/docs/instagram-api) page.
   - Create an app and get the **App ID** and **App Secret**.

2. **Get User Access Token:**
   - After setting up the app, use OAuth to authenticate users and retrieve the access token. You'll need the **user_profile** and **user_media** permissions to access user details.
   - You can refer to [Facebook's OAuth documentation](https://developers.facebook.com/docs/facebook-login/) for details on the authentication flow.

3. **Make API requests:**
   - Once authenticated, you can use the following endpoint to get the user's data:
   
   `https://graph.instagram.com/me?fields=id,username,media_count,account_type&access_token={access-token}`

   Here's an example of how you can use **fetch** to get the data:

```javascript
$('.instagram-get').on( 'click', function(event) {
    let accessToken = 'YOUR_ACCESS_TOKEN';  // Replace with a valid access token
    fetch(`https://graph.instagram.com/me?fields=id,username,media_count,account_type&access_token=${accessToken}`)
    .then(response => response.json())
    .then(data => {
        console.log(data);
        $(".username").html(data.username);
        $(".media-count").html(data.media_count);
        $(".account-type").html(data.account_type);
        $('.insta-details').show('slow');
    })
    .catch(error => console.log('Error fetching Instagram details:', error));
});
```

### Important Notes:
- The new Instagram API only supports user data that you have permission to access (your account or authenticated users).
- You can also fetch media-related data such as recent posts using the media endpoints:
  
  `https://graph.instagram.com/me/media?fields=id,caption,media_url&access_token={access-token}`

### Demo URL (Deprecated)
The demo that previously used the public GraphQL API no longer works, as Instagram now requires OAuth authentication and access tokens. You can check the [Instagram API documentation](https://developers.facebook.com/docs/instagram-api/) for more details on building your app.

![Fetch Instagram Details](https://user-images.githubusercontent.com/26689210/70326031-832ad600-1859-11ea-91a5-e00e16563baa.png)

#### If you are still reading this, :thumbsup: thank you so very much for your time :hourglass:.
:hand: If you are getting any errors, you can create an issue on this repo with proper details.

{{< footer-donation >}}
