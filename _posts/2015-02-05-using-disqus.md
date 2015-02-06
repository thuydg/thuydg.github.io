---
layout: blog
title: Blog comment function
category: blog
tags: [blog]  
summary: How to add comment function to blog
image: http://activerain.trulia.com/image_store/uploads/agents/jaredchristiansen/files/Comment%202.gif
---

# How to add comment to Your Jekyll blog

* There are many choices to add comments function to your blogs. 
* Here is some kind of good choices (in my opinion only). For me I would like to test all of this, but I couldnot so please give me some comments or suggestions about other good ones!

# Facebook comments plugin

* How to?
https://developers.facebook.com/docs/plugins/comments
 - Go to this site and get the code! be sure that you have your own developer profiles with your FB account.

* Goods:
 - Quick and easy
 - Participate easily since almost people have their own FB account now.
* Bads:
 - Not easy to controlled and see what you commented

# Disqus

* How to use?

  1. Add a variable called comments to the YAML Front Matter and set its value to true.
  2. In between a % if page.comments % and a % endif % tag, add the <Universal Embed Code> in the appropriate template where you'd like Disqus to load. 
(https://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions)

* Download: https://disqus.com/