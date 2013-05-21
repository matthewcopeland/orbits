Orbits - WIP
==============

Demo for a stylesheet talk at 2013 ThoughtWorks North America Awayday.

## Demo

### Opening
* This is the final thing we're going for.
* Here's our storyboard.


### The night sky and the 'darken' function
The night sky is a linear-gradient that is based on a single color and utilzes sass' darken function.

The darken (or lighten) function allows you to move through the HSL color-space. This can be quite useful when you want to stay consistent within your color-palette and need to create some contrast.  You'll see this become more useful in the earth.


### The earth
To creat a ball, we'll need an object that is of equal height and width and has a 50% border-radius.


#### Coloring the world
The earth is mostly made of water, so we'll use a blue from our color-palette to color the background-color.


#### Outter glow and inner-shadow
Earth's glow is made utilizing the variable from our color-palette that ended our night-sky, we can create a glow around our earth with a `box-shadow` and sass' `lighten` function.  This maintains consistency with our color-palette while giving the small amount of contrast needed.

For now, we'll use a 2nd css `box-shadow` to create the look of a sphere. Why a shadow instead of a `radial-gradient`? If/when we add some land-masses to the earth, they'll need to receive a consistent shadow.  This is (for now) the easiest way to accomplish this.

#### Size and position driven via variables
The `$earth-size` will come in handy when we need to align things with our planet.  We'll use this variable for `height` and `width` and also to calculate a 50% border-radius.

To center the element horizontally, I've made a small utility that accepts a `$size` and then sets the left and margin-left properties.  This is another use of $earth-size.

Now it's nice and easy to change the size of the planet.



### Rising earth - animation

#### What to animate?
We know that we want the earth to rise from the bottom of the screen to the center of the screen.

#### How to animate?
We're going to accomplish this with css `translate` so that we can get optimize the rendering. Paul Irish on the benefits of animating with translate. http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft.


I will need to know the height of the visible part of the earth.  So we'll calculate the distance of the earth's vertical-offset.  We will now be able to find the visibile height of the earth - this will be useful in a moment.



## References
* Paul Irish on the benefits of animating with translate. http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft.
* Paul Hayes' 3D css sphere http://www.paulrhayes.com/2011-02/creating-a-sphere-with-3d-css.
