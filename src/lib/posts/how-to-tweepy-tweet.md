---
title: "How To Post My First Tweet Programmatically Using Tweepy"
date: "2022-04-10"
updated: "2022-04-10"
categories: 
  - "Twitter"
coverImage: "/images/How-to-post-my-first-tweet-programmatically-using-tweepy.jpg"
coverWidth: 3
coverHeight: 2
excerpt: This post demonstrates how to start tweeting programmatically in python using Tweepy Python library.
---

<script>
  import Callout from '$lib/components/Callout.svelte';
</script>
## Introduction
This blog post shows how to use [Tweepy](https://www.Tweepy.org/) to post your first tweet programmatically.

Covered in this blog post: How to create a Twitter App. How to collect the relevant credentials needed by Tweepy from your Twitter Developer Dashboard. How to use them with Tweepy to post your first tweet with Python code. Code snippet available.

Note that you should use this snippet only for testing and never upload your credentials publicly online.

## Prerequisites
- You should have a [Twitter developer account](https://developer.twitter.com/en/support/twitter-api/developer-account).
- You should have **Python** and **Pip** installed locally.

## Twitter API
We will be using the [Twitter API](https://developer.twitter.com/en/docs/twitter-api/getting-started/getting-access-to-the-twitter-api). Feel free to read it. However, this blog post covers what is needed for the task straight to the point.

## Credentials Needed ( for our case )
In order to tweet programmatically using Tweepy, we need to provide it with 4 credentials. These credentials are used to tell the Twitter API:

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

That's it! Now we have the four credentials we need to provide Tweepy with.

## Python Code Snippet

```python
import random
import Tweepy

consumer_key = "APP_KEY"
consumer_secret = "APP_SECRET"
access_token = "ACCESS_TOKEN"
access_token_secret = "ACCESS_TOKEN_SECRET"
    
print("Authenticate")
auth = Tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = Tweepy.API(auth)

tweet = "Refrigerator Test Hello World!"
print(f"Post tweet: {tweet}")
api.update_status(tweet)
```

Execute this Python code, and voila! you just tweeted "Refrigerator Test Hello World!" to the Twitter timeline!

Click on that Tweet and Observe your App's name being displayed instead of 'Twitter Web App', 'Twitter for iPhone' or 'Twitter for Android'.