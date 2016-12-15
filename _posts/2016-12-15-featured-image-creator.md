---
layout: post
title: Create a nice blog featured image in 30 seconds
comments: True
summary: In this post I show a tool I built to easily create images. I typically use it to generate featured blog images. I started this tool a few years ago, but this iteration made it much better. I added the ability to save the image, and use some nice JS to select background images from different themes.
categories: [Projects]
tags: [Javascript, Jquery, CSS, PHP, design, images, blog, featuredimage, materialdesign]
image: featured-image-creator.jpg
---

<h3>Featured image creator</h3>

I created the [Featured image creator](http://projects.bobbelderbos.com/featured_image) to automate featured image creation for my blog. You can of course use it for any image creation. I works by selecting a background theme (material design or bamboo, more themes to be added ...), select a title and font and optionally a second background image. Instead of the fixed themes you can put any image url in the two image fields. You can download and bookmark the image. Here is how it works:

![quick tour]({{ site.baseurl }}/assets/feat_img1.gif)

Featured image for this post:

![quick tour]({{ site.baseurl }}/assets/featured/featured-image-creator.jpg)

Or lets match the font of the tool (Montez, cursive):

![quick tour]({{ site.baseurl }}/assets/featured/featured-image-creator_alt1.jpg)

Or be a bit more creative add the tool's logo as a second background imge: 

![quick tour]({{ site.baseurl }}/assets/featured/featured-image-creator_alt2.jpg)

I also created the logo of the tool with it:

![quick tour](http://projects.bobbelderbos.com/featured_image/i/logo.png)

<h3>What is it doing under the hood?</h3>

This is mostly JS (jQuery) listening to form field changes and taking their changed values, updating the CSS of the canvas on the right in real-time. What I think is the coolest thing I achieved is the theme background option dropdown that pops out when you select the backgound image cell:

![pick your background]({{ site.baseurl }}/assets/feat_img_bg_theme.png)

Pick one and the canvas background updates instantly.

So there is a good deal of CSS as well and some PHP to deal with the form handling and querying the theme background images. Saving the image was a bit of a challenge, but [html2canvas](https://html2canvas.hertzen.com/) made it much easier. For blocking the UI while processing (see next gif), I use [jQuery BlockUI](http://malsup.com/jquery/block/). 

One issue I had to try/catch was a tainted canvas, this is when you use external images: 

![error handling in case of tainted canvas]({{ site.baseurl }}/assets/feat_img_tainted.png)

In that case the Save button does not automatically download the image, it creates the image alongside the canvas and you have to manually right-click and save it. The proxy option of the plugin did not work for me in this case.

See [this issue](https://github.com/niklasvh/html2canvas/issues/103) and [html2canvas FAQ](https://html2canvas.hertzen.com/faq.html).

Here is a more complete exmample with an second background image:

![quick tour]({{ site.baseurl }}/assets/feat_img2.gif)

I used [this awesome online tool](http://gifmaker.me/) to create the gif animations for this post.

<h3>Result</h3>

Consistent look on my blog's homepage:

![consistency]({{ site.baseurl }}/assets/feat_img_consistency.png)

If you like this feel free to [try it out](http://projects.bobbelderbos.com/featured_image/) and let me know what you think ...
