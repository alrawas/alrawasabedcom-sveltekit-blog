---
title: "How to post your first tweet programmatically using tweepy"
date: "2022-04-08"
updated: "2022-04-08"
categories: 
  - "Twitter"
coverImage: "/images/How-to-post-my-first-tweet-programmatically-using-tweepy.jpg"
coverWidth: 16
coverHeight: 9
excerpt: This post demonstrates how to start tweeting programmatically in python using tweepy
---

<script>
  import Callout from '$lib/components/Callout.svelte';
</script>
## Introduction
This blog post shows how to use tweepy to post your first tweet programmatically.

Covered in this blog post: How to create a Twitter App. How to collect the relevant credentials needed by tweepy, from your Twitter Developer Dashboard. How to use them with tweepy, with the code snippet available.

Note that you should use this snippet only for testing and never upload your credentials publicly online.

## Prerequisites
- You should have a [Twitter developer account](https://developer.twitter.com/en/support/twitter-api/developer-account).
- You should have **Python** and **Pip** installed locally.

## Twitter API
We will be using [Twitter API](https://developer.twitter.com/en/docs/twitter-api/getting-started/getting-access-to-the-twitter-api). Feel free to read it. However, this blog post covers what is needed for tha task straight to the point.

## Credentials Needed ( for our case )
In order to tweet programmatically using tweepy, we need to provide it with 4 credentials. These credentials are used to tell the Twitter API:

1. Which app we are using: **API Key**
2. Proof that we own the app: **API Key Secret**
<Callout>
Think of these as the user name and password that represents your App when making API requests.
</Callout>

3. Which Twitter account is going to be used to Tweet: **Access Token**
4. A Password for that Access Token: **Access Token Secret**
<Callout>
An Access Token and Secret are user-specific credentials used to authenticate OAuth 1.0a API requests. They specify the Twitter account the request is made on behalf of.
</Callout>

## Create a Twitter App and Obtain the credentials
1. Go to your [Twitter Dashboard Portal](https://developer.twitter.com/en/portal/dashboard)
2. On the sidebar, Click **Projects & Apps -> Overview**
2. Create a Standalone App
<!-- ![Click on create app](/images/twitter-api-create-app.png "Click on create app") -->
3. Name your app, click next
4. Save the provided keys (<span style="color:var(--accent)">**API Key**</span>, and <span style="color:var(--accent)">**API Key Secret**</span>. We will not use **Bearer**)
5. Go to **App Settings**
6. Click **Setup Auth**
    1. Enable **OAuth 1.0a**
    2. Set **app permissions** to Read and write
    3. Set **Callback Uri** and **Redirect URL** to a valid website ex. https://google.com
    4. Save
7. Navigate to **Keys And Tokens** Tab for the app.
    - Under Authentication tokens, Generate an **Access Token and Secret** (for your dev account)
    - Copy the <span style="color:var(--accent)">**Access Token**</span> and <span style="color:var(--accent)">**Secret**</span> somewhere safe
    - We can ignore the **Bearer** for this tutorial

That's it! Now we have the four credentials we need to provide tweepy with.

## Code

```python
import random
import tweepy

consumer_key = "APP_KEY"
consumer_secret = "APP_SECRET"
access_token = "ACCESS_TOKEN"
access_token_secret = "ACCESS_TOKEN_SECRET"
    
print("Authenticate")
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth)

tweet = "Refrigerator Test Hello World!"
print(f"Post tweet: {tweet}")
api.update_status(tweet)
```

Execute this Python code, and voila! you just tweeted "Refrigerator Test Hello World!" to the Twitter timeline!