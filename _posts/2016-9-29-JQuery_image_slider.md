---
layout: post
title: JQuery Image Slider
---

Here is a quick and dirty way to build a basic image slider using JQuery.

The way this image slider will work is that we will have a seamless horizontal list of images that we want to be displayed. We will use JQuery to increment the margin of this list when a button is clicked, sliding to the previous or next image. 

- First we will begin with the HTML markup.

```html
<div id="imageSlider">
	<ul class="images">
		<li class="image"><img src="http://cdn.wonderfulengineering.com/wp-content/uploads/2014/04/space-wallpapers-9.jpg"></li>
		<li class="image"><img src="http://wallgallery.org/wp-content/uploads/2016/05/Space-hd.jpg"></li>
		<li class="image"><img src="http://img.phombo.com/img1/photocombo/5912/602_HD_Space_wallpapers_Various_Sises-18.jpg_Leo.jpg"></li>
		<li class="image"><img src="https://images8.alphacoders.com/397/397989.jpg"></li>
	</ul>
</div>
```


<!-- ![_config.yml]({{ site.baseurl }}/images/config.png) -->

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.