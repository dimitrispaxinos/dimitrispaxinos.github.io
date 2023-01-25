---
layout: post
title: How I increased my WordPress site’s performance from 31 to 92 in less than 2 hours
tags: seo wordpress optimization
description: A post about optimizing a website's performance
---


I admit it; I am completely new to SEO and web page optimization. SEO and SEM (Search Engine Marketing) are valuable skills for every (wannabe) solopreneur/enterpreneur. As an engineer, I tend only to build and… keep building. The problem is that building a product is nice but not enough if no one knows about it. This is where SEO comes into play.

Therefore, learning SEO was one of my goals for 2023 as I have both [my software consultancy - Apptiva Software](https://apptivasoftware.com) with a very basic and unoptimized website as well as some ideas about products that I would like to build and promote.

 **So, how do you start?**

  There are many ways to dive into it; I chose Youtube and, more specifically [Ahrefs’ SEO Course for Beginners amazing video](https://www.youtube.com/watch?v=xsVTqzratPs&ab_channel=Ahrefs) that I would recommend to anyone wanting to learn SEO.

After watching the complete tutorial for almost two hours, the next step was to start practicing what I had learned. Apptiva’s website was a really good case for trying it out.

Everything started with testing the site on [PageSpeed Insights](https://pagespeed.web.dev/). According to Google, the website’s performance on mobile is what actually counts more. So, I checked it out… and was shocked! I should not be proud of it, I know!
  
  ![PageSpeed before fine tuning picture](https://github.com/dimitrispaxinos/dimitrispaxinos.github.io/blob/master/_assets/images/apptiva_performance_before.png?raw=true)


This had to change! Following the [Pareto principle](https://en.wikipedia.org/wiki/Pareto_principle) (80/20 rule), I wanted to go for the low-hanging fruit and a quick win. This is why I watched one more (shorter) Ahrefs video, [How to Speed Up Your WordPress Website (Simple Guide)]([https://www.youtube.com/watch?v=BrY6a-lsLp8&t=365s&ab_channel=Ahrefs) and followed the instructions. 

The action plan below is based on this video. It took me less than 2 hours, and the results were more than amazing.

 

## Enable Cloudflare
  
Cloudflare is a Content Delivery, Network (CDN) which basically stores your website in different places around the world so that each request fetches the data from the geographically closest server. Cloudflare has a free plan that would be enough for your needs.     

## WP Rocket Plugin

WP Rocket ([https://wp-rocket.me/](https://wp-rocket.me/)) is a WordPress caching plugin that boosts your loading time, improves your PageSpeed score, and optimizes your Core Web Vitals.  The entry price of $59 is a true bargain.  
![WP Rocket Logo](https://github.com/dimitrispaxinos/dimitrispaxinos.github.io/blob/master/_assets/images/wp-rocket-logo.png?raw=true)

Once you buy it and install it, go to settings and modify settings according to the screenshots below. 

### Cache

All you need to do here is enable caching for mobile devices


![WP Rocket Cache Settings](![wp_rocket_cache.png](https://github.com/dimitrispaxinos/dimitrispaxinos.github.io/blob/master/_assets/images/wp_rocket_cache.png?raw=true)

### Media

Check everything here apart from the "Add missing image dimensions" checkbox

![WP Rocket Media Settings](https://github.com/dimitrispaxinos/dimitrispaxinos.github.io/blob/master/_assets/images/wp_rocket_file_media.png?raw=true)

### File Optimization

There are two sections, CSS and Javascript. Let' start with the CSS part where we select everything. 

![WP Rocket File Optimization CSS](https://github.com/dimitrispaxinos/dimitrispaxinos.github.io/blob/master/_assets/images/wp_rocket_file_optimization_css.png?raw=true)

The same applies to Javascript

![WP Rocket File Optimization CSS](https://github.com/dimitrispaxinos/dimitrispaxinos.github.io/blob/master/_assets/images/wp_rocket_file_optimization_javascript.png?raw=true)


## Image Optimization

Minimizing/compressing your images can dramatically increase your website's speed. This is why we are going to use one more plugin, free this time. [Robin image Optimizer](https://wordpress.org/plugins/robin-image-optimizer/#why%20is%20this%20plugin%20free%20and%20how%20long%20it%20will%20be%20this%20way%3F) can scan through your website and compress all your images. It is free since it uses a free compression web service.

Once you install it, all you have to do is press 'Optimize' and let it do its magic. The screenshot below show how it improved the images of my website. Impressive results I would say!


![Robin Image Optimizer Screenshot](https://github.com/dimitrispaxinos/dimitrispaxinos.github.io/blob/master/_assets/images/robin-image-optimizer-screenshot.png?raw=true)



## Result

We are ready! We jumped from 31 to 92 in less than 2 hours. It was definitely  worh the investment!

![PageSpeed after fine tuning picture](https://github.com/dimitrispaxinos/dimitrispaxinos.github.io/blob/master/_assets/images/apptiva_performance_after.png?raw=true)
