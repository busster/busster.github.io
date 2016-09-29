---
layout: post
title: JQuery Image Slider
---

Here is a quick and dirty way to build a basic image slider using JQuery.

As an FYI, this is my first ever blogpost!

The way this image slider will work is that we will have a seamless horizontal list of images that we want to be displayed. We will use JQuery to increment the margin of this list when a button is clicked, sliding to the previous or next image. 


## First we will begin with the HTML markup.

```html
<button id="prev" type="button">prev</button>
<button id="next" type="button">next</button>
<div id="imageSlider">
	<ul class="images">
		<li class="image"><img src="http://cdn.wonderfulengineering.com/wp-content/uploads/2014/04/space-wallpapers-9.jpg"></li>
		<li class="image"><img src="http://wallgallery.org/wp-content/uploads/2016/05/Space-hd.jpg"></li>
		<li class="image"><img src="http://img.phombo.com/img1/photocombo/5912/602_HD_Space_wallpapers_Various_Sises-18.jpg_Leo.jpg"></li>
		<li class="image"><img src="https://images8.alphacoders.com/397/397989.jpg"></li>
	</ul>
</div>
```

- Here we created some buttons, that will allow us to slide to either the previous or next image.
- Next created a div container with the id `imageSlider` 
	- This acts essentially as a 'picture frame' and will hide the other pictures in the list, only displaying the current one
- Next we created an unordered list  with the class of `images`
- Inside this list we have list items with the class of `image` that contain our image.
	- I have just added some space images as placeholders, plus added bonus the pictures are dope.


## Next we will add some CSS styling.

```css
#imageSlider {
	overflow: hidden;
	height: 250px;
  	width: 500px;
}
#imageSlider .images {
	display: block;
	margin: 0;
	padding: 0;
	height: 250px;
  	width: 2000px;
}
#imageSlider .image {
	float: left;
	list-style-type: none;
	height: 250px;
  	width: 500px;
}
img {
	width: 100%;
}
```

- Important things to note about styling are the height and width of each element.
	- Each image is the same height and width as the div container. 
	- This is so that the image fills the entire container and we do not see any of the adjacent images.
	- The list of images is the width of all of the images combined so that we can use the margin to slide the image left or right.
- We use `overflow: hidden;` to hide anything outside of the extents of the container so only the image centered on the container will be visible.
- We also make the list of images a block level element and float each image to the left so they stack horizontally on eachother.


## Next we will add the JQuery to give the slider functionality

- We want this slider to be functional as soon as the page is loaded so we can declare our code inside a function that is called after the page loads. 

```javascript
$(document).ready(function(){

});
```

- Next we will need some information to use within our code.
	- We will need access to our unordered list of images so we can animate those to slide left or right to reveal an image.
	- we will also need to set some variables to be used

- To get access to our HTML elements we can use create JQuery variables that reference those DOM elements.

```javascript
$(document).ready(function(){

	var $imageSlider = $('#imageSlider');
	var $imageContainer = $imageSlider.find('.images');
	var $images = $imageContainer.find('.image');
	var $imagesAmt = $images.length

});
```

- Here we have set four JQuery variables:
1. `$imageSlider` references our main div with `id="imageSlider"`
2. `$imageContainer` searches through our "imageSlider" div to find our unordered list with `class="images"`
	- This is what we will animate left or right with our function
3. `$images` searches through our "images" unordered list to find each list item with `class="image"`
4. `$imagesAmt` gets the length of the list items, or how many images are in the list.

- Next we declare some more variables that we will need to use

```javascript
$(document).ready(function(){

	var width = 500;
	var animationSpeed = 1000;
	var currentImage = 0;

	var $imageSlider = $('#imageSlider');
	var $imageContainer = $imageSlider.find('.images');
	var $images = $imageContainer.find('.image');
	var $imagesAmt = $images.length

});
```

- Here we added three more variables:
1. a width variable, the width of each image, to be used to update the margin of our $imagesContainer
2. an `animationSpeed` which will control the time it takes for the animation to complete.
3. a `currentImage` variable so that the function can know the 'index' of the current image. This will be used to multiply the width of the image to set the margin.

- Now that we have our variables lets write the function:

```javascript
function slideImage() {
	$imageContainer.animate({'margin-left': (-1 * (currentImage)) * width}, animationSpeed);
};
```

- So this is the function that we will call to slide the image left or right.
- We delcare the function `slideImage()`
- we use `$imageContainer.animate` to access our `.images` class in the DOM and call an animation on it. 
- In the animation we need a two things.
	1. We need to express the CSS property we want to animate
	2. We need to delcare over what duration we are going to animate
- Here we want to update the `margin-left` property. 
	- Incrementing this propety by the width of the image will have the effect of moving the list of images to display whatever image is next.
	- So, we want to use our `currentImage` index and multiply it by the width of the image. Also, we multiply our index by -1 to create a negative number for reasons you will see later. 
- Also we use our `animationSpeed` variable to set the duration of the animation

- Essentially what this does is use the index in the list of the image that is to be displayed, and multiply that by the width of each image so that we can set the margin to that number. This shifts the list of images to that image.

- This is great but we need a way to update `currentImage` with our buttons so that we can call this function

```javascript
$('#next').click(function(){
	currentImage += 1;
	if (currentImage > $imagesAmt - 1) {
		currentImage = 0
	}
	slideImage();
});

$('#prev').click(function(){
	currentImage -= 1;
	if (currentImage < 0 ) {
		currentImage = $imagesAmt - 1;
	}
	slideImage();
});
```

- We create two functions: One for our prev and next buttons
- We access them in the DOM by using their id's `#next` and `#prev`
- We use `.click` so that we can run a function anytime those buttons are clicked by the user
- For our function we want to update the `currentImage` to the previous or next index in the list and then call the `slideImage()` function to execute the animation.
- So for NEXT we want to increment the index by 1.
	- We add some logic to handle the edge case. 
	- If the current index is greater than the amount of images then set the index back to the first image. This just loops the gallery back to the beginning.
- For PREV we do the same thing but in reverse.
	- We decrement the index by 1. 
	- If the index is less than 0 set the index to the last image.
- At the end of our functions we call `slideImage()` so that we can execute the animation.

- Your finished javascript should look something like this!

```javascript
$(document).ready(function(){
	var width = 1000;
	var animationSpeed = 1000;
	var currentImage = 0;

	var $imageSlider = $('#imageSlider');
	var $imageContainer = $imageSlider.find('.images');
	var $images = $imageContainer.find('.image');
	var $imagesAmt = $images.length

	function slideImage() {
			$imageContainer.animate({'margin-left': (-1 * (currentImage)) * width}, animationSpeed);
	};

	$('#next').click(function(){
		currentImage += 1;
		if (currentImage > $imagesAmt - 1) {
			currentImage = 0
		}
		slideImage();
	});

	$('#prev').click(function(){
		currentImage -= 1;
		if (currentImage < 0 ) {
			currentImage = $imagesAmt - 1;
		}
		slideImage();
	});
});
```

## Final notes

- Some further CSS can be used to position the buttons in a more logical fashion. You could exchange the buttons for a png of an arrow and place it ontop of the slider container. You could add some further CSS or JQuery rules to make that image dynamic on hover or click.
- Also, this really only works if all of the images are relatively the same size. Otherwise you could have some clipping of the top and bottom of the image or it might not fill the entire div container. You could add some further javascript logic to handle some of these cases though. 
- Also, when you get to the end of the list instead of moving from left to right to the first image, it slides all the way back through all of them. One way to change this would be to add the first image again at the end of the list and update the margin instantaneously after the animation takes place. So that when you are on that image it sets the margin to that image at the begining or end of the list. This change would be imperceptible to the user.

- Cheers! Hopefully this helped!


<!-- ![_config.yml]({{ site.baseurl }}/images/config.png) -->

