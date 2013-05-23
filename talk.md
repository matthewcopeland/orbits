Talk for Awayday
===================

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

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/01.png)

### Rising earth - animation

#### What to animate?
Position, gradient and glow.



For each animation, the `animation-duration` should be extacted into a variable. This will be beneficial when it comes time to sync a few of them up.

##### Position
We know that we want the earth to rise from the bottom of the screen to the center of the screen. The earth's resting place is already in the center of our screen. So we only need to move it `from` another position. See [Lea Varou's article on single-keyframe animations](http://lea.verou.me/2012/12/animations-with-one-keyframe).

We'll accomplish this with css `translate` so that we can get optimize the rendering. See [Paul Irish's article on translate v pos-abs](http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft).




## References
* Paul Irish on the benefits of animating with translate. http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft
* Lea Verou's animation's with one keyframe. http://lea.verou.me/2012/12/animations-with-one-keyframe
* Paul Hayes' 3D css sphere http://www.paulrhayes.com/2011-02/creating-a-sphere-with-3d-css
