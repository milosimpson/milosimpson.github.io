---
layout: post
published: true
title: Setting up the ability to add photos to entries
---
## Reference

Did not work OOTB for me.  

- [https://blog.webjeda.com/edit-posts-jekyll/](https://blog.webjeda.com/edit-posts-jekyll/)
- [https://github.com/prose/prose/wiki/Prose-Configuration](https://github.com/prose/prose/wiki/Prose-Configuration)

I think the main problem was that I was trying to have put photos in a "\_media" dir, which Jekyll treats as "special" as it begins with an underscore.

## Configure Prose more in the Jekeyll config.yaml

So Prose can be configured vai yaml to 
- know about the default media directory / where to put files you want to upload
- have nice defaults for new documents for each of your "sections"

## If this works ...

![2018-01-28-AlamoDraftHouse-door-to-nowhere.jpg]({{site.baseurl}}/media/posts/2018-01-28-AlamoDraftHouse-door-to-nowhere.jpg)

Then WIN!

This is a door to nowhere on the backside of a "new" Alamo Drafthouse in Austin.
