Talk for Awayday
===================

Demo for a stylesheet talk at 2013 ThoughtWorks North America Awayday.


## Demo

### Opening
* This is the final thing we're going for.
* Here's our storyboard.


### The night sky and the 'darken' function
The night sky is a linear-gradient that is based on a single color and utilzes sass' darken function.

The darken (or lighten) function allows you to move through the HSL color-space. This can be quite useful when you want to stay consistent within your color-palette and need to create some contrast.  You'll see this become more useful in the Earth.


## The Earth
To creat a ball, we'll need an object that is of equal height and width and has a 50% border-radius.


#### Coloring the world
The Earth is mostly made of water, so we'll use a blue from our color-palette to color the background-color.


#### Outter glow and inner-shadow
Earth's glow is made utilizing the variable from our color-palette that ended our night-sky, we can create a glow around our Earth with a `box-shadow` and sass' `lighten` function.  This maintains consistency with our color-palette while giving the small amount of contrast needed.

For now, we'll use a 2nd css `box-shadow` to create the look of a sphere. Why a shadow instead of a `radial-gradient`? If/when we add some land-masses to the Earth, they'll need to receive a consistent shadow.  This is (for now) the easiest way to accomplish this.

#### Size and position driven via variables
The `$Earth-size` will come in handy when we need to align things with our planet.  We'll use this variable for `height` and `width` and also to calculate a 50% border-radius.

To center the element horizontally, I've made a small utility that accepts a `$size` and then sets the left and margin-left properties.  This is another use of $Earth-size.

Now it's nice and easy to change the size of the planet.

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/01.png)




## Rising Earth animation

We know that we want the Earth to rise from the bottom of the screen to the center of the screen. The Earth's resting place is already in the center of our screen. So we only need to move it `from` another position. See [Lea Varou's article on single-keyframe animations](http://lea.verou.me/2012/12/animations-with-one-keyframe).

We'll accomplish this with css `translate` so that we can get optimize the rendering. See [Paul Irish's article on translate v pos-abs](http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft).

The `animation-duration` should be extacted into a variable. This will be beneficial when it comes time to sync a few of them up.



## The moon

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/02-earth-and-moon.png)


### Base `$moon-size` on `$earth-size`.
The Moon is approximately 27% the size of the Earth. So as you guessed, we'll be using that math to create our Moon.


### Make a utility for a sphere
Since we're making yet another sphere that is a sphere, it seems like time to make a utility for this.  Let's make a mixin for a sphere and use it for our Earth and Moon. This is going to be pretty big, so I'm going to put into a new file.  We can keep all of our general planetary-ish things here.

In this utility, we'll need to include a few things: `height`, `width`, `border-radius`, and a `@function` for the sphere's inset `box-shadow`.

#### The sphere shadow function
We can reuse the logic from our earth shadow. Sorta nice that we used variables at the time, right?

***Why function vs variable?*** Because we're going to pass this function the `$size` of the sphere and let it adjust our inset-shadow accordingly.

***Why function vs mixin?*** Because we don't want to return the full `box-shadow` property.  We only want to return the value for that `box-shadow`. This way, we can still give the earth multiple shadows, while the Moon can have a single shadow.




#### The sphere utility
```scss
// first you must make a circle.
// we'll keep this seperate for easy reuse.

@mixin circle($size) {
  display: block;
  height: $size;
  width: $size;
  @include border-radius($size/2);
}



// shadows
@function sphere-inset-shadow($size) {
  @return inset (-$size/20) (-$size/20) $size/10 0 rgba(0,0,0, 0.6);
}



@mixin sphere($size) {
  @include circle($size);
  box-shadow: sphere-inset-shadow($size);
}
```




#### Using the sphere utility
```scss
$earth-size: 600px;
#earth {
  @include circle($earth-size);
  box-shadow: $earth-outter-glow, sphere-inset-shadow($earth-size);
}



$moon-size: $earth-size*0.27;
#moon {
  @include sphere($moon-size);
}

```


## Rising moon animation

### Simple start
For starters, the moon will be very simple.  We'll have a full-moon come out from one side of the Earth, pass in front of the Earth and then set behind the Earth.  We'll drive this with variables so that we can change it up as we gain information about the real proportions of the Earth and moon.

Comment out the rising-earth animation for now so that we can work with something that isn't yet moving. We'll sync this up in a minute.


Position the Moon in the center of the screen, behind the Earth. (Make center-mixin and mention the zed_index file).


```scss
// _moon.scss

$moon-orbit-duration: 6s;

@include keyframes(orbit) {
  25% {
    z-index: $moon-z;
    @include transform( translateX(-$earth-size) );
  }


  26% { z-index: ($earth-z + 1); } // what is this doing here?


  75% {
    z-index: ($earth-z + 1);
    @include transform( translateX($earth-size) );
  }


  76% { z-index: $moon-z; } // what is this doing?
}


#moon {
  position: fixed;
  z-index: $moon-z;
  @include center($moon-size);
  @include animation( orbit $moon-orbit-duration infinite linear );
}

```

***

### Result

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/moon-animation/moon-animation-01.jpg)

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/moon-animation/moon-animation-02.jpg)

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/moon-animation/moon-animation-03.jpg)

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/moon-animation/moon-animation-04.jpg)

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/moon-animation/moon-animation-05.jpg)

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/moon-animation/moon-animation-06.jpg)

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/moon-animation/moon-animation-07.jpg)


***

### Moon orbit - step it up with real galactic ratios
The moon's orbit is % of the Earth's mass. So we'll replace the `translateX($earth-size)` with `translateX($moon-orbit-radius)`.



## References

### CSS stuff
* Paul Irish on the benefits of animating with translate. http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft
* Lea Verou's animation's with one keyframe. http://lea.verou.me/2012/12/animations-with-one-keyframe
* Paul Hayes' 3D css sphere http://www.paulrhayes.com/2011-02/creating-a-sphere-with-3d-css


### Galactic stuff
* http://solarsystem.nasa.gov/planets/profile.cfm?Display=Facts&Object=Moon
* http://en.wikipedia.org/wiki/Moon
* http://www.universetoday.com/20489/moon-compared-to-Earth
