Orbits
========

Demo for a stylesheet talk at 2013 ThoughtWorks North America Awayday.


## Opening
* This is the final thing we're going for.
* Here's our storyboard.


## The night sky and the 'darken' function
The night sky is a linear-gradient that is based on a single color and utilzes sass' darken function.

The darken (or lighten) function allows you to move through the HSL color-space. This can be quite useful when you want to stay consistent within your color-palette and need to create some contrast.  You'll see this become more useful in the earth.


## The earth
To creat a ball, we'll need an object that is of equal height and width and has a 50% border-radius.

### Variable driven-size
This is a convenient spot to use a variable to drive the size. The `$earth-size` will come in handy when we need to align things with our planet.  We'll use this variable for `height` and `width` and also to calculate a 50% border-radius.

### Positioning the earth
To center the element horizontally, I've made a small utility that accepts a `$size` and then sets the left and margin-left properties.  This is another use of $earth-size.

I'm not sure how much of the earth I'll want to be showing when it comes time to animate it, but I will need to know the height of the visible part of the earth.  So for now, I'll use a variable that calculates the distance to vertically-offset the earth.  I will now be able to find the visibile height of the earth - this will be useful in a moment.


### Coloring the world
* The earth is mostly made of water, so we'll use a blue from our color-palette to color the background-color.


* Earth's glow is made utilizing the variable from our color-palette that ended our night-sky, we can create a glow around our earth with a `box-shadow` and sass' `lighten` function.  This maintains consistency with our color-palette while giving the small amount of contrast needed.
