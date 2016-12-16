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

I created the [Featured image creator](http://projects.bobbelderbos.com/featured_image) to automate featured image creation for my blog. You can of course use it for any image creation. I works by selecting a background theme (material design or bamboo, more themes to be added ...), select a title and font and optionally a second background image. Instead of the fixed themes you can put any image url in the two image fields. You can save (download), bookmark and tweet the created image. Here is how it works:

![quick tour]({{ site.baseurl }}/assets/feat_img1.gif)

Featured image for this post:

![quick tour]({{ site.baseurl }}/assets/featured/featured-image-creator.jpg)

OK lets change the BG and match the font of the tool's title at the top (Montez, cursive):

![quick tour]({{ site.baseurl }}/assets/featured/featured-image-creator_alt1.jpg)

... or be a bit more creative add the tool's logo as a second background imge: 

![quick tour]({{ site.baseurl }}/assets/featured/featured-image-creator_alt2.jpg)

I also created the logo of the tool with it:

![quick tour](http://projects.bobbelderbos.com/featured_image/i/logo.png)

<h3>What is it doing under the hood?</h3>

This is mostly JS (jQuery) listening to form field changes and taking their changed values, updating the CSS of the canvas on the right in real-time. What I think is the coolest thing I achieved is the theme background option dropdown that pops out when you select the backgound image cell:

![pick your background]({{ site.baseurl }}/assets/feat_img_bg_theme.png)

I use the [jQuery UI's autocomplete](https://jqueryui.com/autocomplete/) for this: 

	function theme_autocomplete(){
		$( "#bg1_url" ).autocomplete({
			dataType: "json",
			source: "files.php?theme=" + $("#collection option:selected").val(),
			minLength: 0,
			search: function(event, ui) {
			$('.spinner').show();
			},
			open: function(event, ui) {
			$('.spinner').hide();
			},
			select: function(event, ui) {
			event.preventDefault();
			$(this).val(ui.item.full);
			$('#featImg').css({"background-image": "url("+ui.item.full+")" });
			}
		}).focus(function() { // show all upon focus of ac field
			$(this).autocomplete('search', $(this).val())
		}).data( "autocomplete" )._renderItem = function( ul, item ) {
			var imghtml = '';
			imghtml += "<a id="+item.full+">";
			imghtml += "<img src='"+item.thumb+"'>";
			imghtml += "</a>";
			return $( "<li></li>" )
			.data( "item.autocomplete", item )
			.append(imghtml)
			.appendTo(ul);
		};
	}
	...
	...

	(function($){
		// not most elegant, but need the auto-complete dynamically pick collection type
		theme_autocomplete();                                                                                                                               
		$('#collection').on('change', function(e) {
			theme_autocomplete();
		});
	})(jQuery);

Pick one and the canvas background updates instantly.

So there is a good deal of CSS as well and some PHP to deal with the form handling and querying the theme background images. Saving the image was a bit of a challenge, but [html2canvas](https://html2canvas.hertzen.com/) made it much easier. For blocking the UI while processing (see next gif), I use [jQuery BlockUI](http://malsup.com/jquery/block/). 

One issue I had to try/catch was a tainted canvas, this is when you use external images: 

![error handling in case of tainted canvas]({{ site.baseurl }}/assets/feat_img_tainted.png)

In that case the Save button does not automatically download the image, it creates the image alongside the canvas and you have to manually right-click and save it. The proxy option of the plugin did not work for me in this case.

See [this issue](https://github.com/niklasvh/html2canvas/issues/103) and [html2canvas FAQ](https://html2canvas.hertzen.com/faq.html).

Here is a more complete example with an second background image:

![quick tour]({{ site.baseurl }}/assets/feat_img2.gif)

I used [this awesome online tool](http://gifmaker.me/) to create the gif animations for this post.

<h3>Result</h3>

Consistent look on my blog's homepage:

![consistency]({{ site.baseurl }}/assets/feat_img_consistency.png)

If you like this feel free to [try it out](http://projects.bobbelderbos.com/featured_image/) and let me know what you think ... And use the Tweet button to share your creations on Twitter using hashtag #FeaturedImageCreator 
