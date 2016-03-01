---
layout: post
summary: Force the Facebook crawler to re-fetch your link
tags: Facebook programming
---
Force the Facebook crawler to re-fetch your data:

https://developers.facebook.com/docs/sharing/opengraph/using-objects#update

> The Facebook crawler will re-scrape (and therefore update) objects:
> 
> When the object URL is input in the Object Debugger Every 30 days
> after the first scrape When an app triggers a scrape using an API
> endpoint This Graph API endpoint is simply a call to:

    `POST /?id={object-instance-id or object-url}&amp;scrape=true`

> The id parameter can be either the canonical URL of your object or the
> ID of the object instance in the graph.
