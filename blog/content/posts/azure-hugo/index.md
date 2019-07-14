---
title: "How to build your a static site with Hugo"
date: 2019-07-13T20:38:49-04:00
draft: false
type: "post"
description: "Using Hugo to create a static site hosted on Azure storage"
tags: ["azure", "hugo"]
---

In a pair of previous posts I described how to [host a static site in Azure storage](../azure-site) and also how to [use a CDN to map a custom domain to your site with https](../azure-cdn). For each of those examples I used a simple 'hello world' html page as the site. In the real world we are going to want more out of our site. In my research I came across [Hugo](https://gohugo.io/) and decided to give it a go.

---

## What is Hugo?
Hugo is an open source static site generator. If you really want to be sold on it, go browse [their docs](https://gohugo.io/about/) to learn everything you might want to know. As an end-user, Hugo is great because:

- It uses a simple Go-based templating engine to layout your site.
- The number of templates available to download and use means you can get started quickly.
- You write all of your content in markdown.
- Hugo has shortcodes to add flexibility where markdown is not sufficient.
- Its CLI makes it easy to run your site local and generate content to deploy to production.

If you are interested in giving it a try, then read on. But first, you need to install Hugo. Follow the [instructions here](https://gohugo.io/getting-started/installing) and then come back.

---






