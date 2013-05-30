Talk for Awayday
===================

Demo for a stylesheet talk at 2013 ThoughtWorks North America Awayday.


## Opening
* Here's what we're going for: http://youtu.be/CI5oZjKps-w


## Space

### The 'darken' function
The night sky utilzes sass' darken function. The darken (or lighten) function allows you to move through the HSL color-space. This can be quite useful when you want to stay consistent within your color-palette and need to create some contrast.  You'll see this become more useful in the Earth.


## The Sun

To create a ball, we'll need an object that is of equal height and width and has a 50% border-radius.


### Size and position driven via variables
The `$planet-size` will come in handy when we need to align things with our planet. We'll use this variable for `height` and `width` and also to calculate a 50% border-radius. To center the element horizontally, I've made a small utility that accepts a `$size` and then sets the left and margin-left properties. This is another use of $planet-size. Now it's nice and easy to change the size of the planet.


### Make a utility for a Cicle
In this utility, we'll need to include a few things: `height`, `width`.

```scss
@mixin circle($size) {
  display: block;
  height: $size;
  width: $size;
  @include border-radius($size/2);
}
```


## Orbits
Before we can make a planet, we need to make an orbit. The orbit is what we'll be rotating around the sun.

* Based on $sun-size.
* Center it.
* add the orbit-animation.



## The Planets
* Add the planet.
* Give the planet a default position.
* Shade the planet with an inset box-shadow.



## Animation timing
* Setup variables for the animation's arguments.
* Hook the animations together in the variables file.
* Use the sum total of previous animation to determine when to execute the next animation.
* PLAY TIME! Have fun tweaking stuff.


## Add the text-overlay animation.
* Use the sum of the animation time.
* Count the number of subtitles.
* Use nth-of-type to fade them in and out.




## References

### CSS stuff
* Paul Irish on the benefits of animating with translate. http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft
* Lea Verou's animation's with one keyframe. http://lea.verou.me/2012/12/animations-with-one-keyframe
* David DeSandro on 3D transforms http://24ways.org/2010/intro-to-css-3d-transforms
* W3 http://www.w3.org/TR/css3-transforms
* Paul Hayes' 3D css sphere http://www.paulrhayes.com/2011-02/creating-a-sphere-with-3d-css
* Custom sass script http://victorcoulon.fr/generating-random-color-in-sass and http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#adding_custom_functions
* Bourbon http://bourbon.io

### Galactic stuff
* http://solarsystem.nasa.gov/planets
* http://en.wikipedia.org/wiki/Moon
* http://www.universetoday.com/20489/moon-compared-to-Earth
