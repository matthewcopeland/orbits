Orbits talk
=============

A stylesheet talk at 2013 ThoughtWorks North America Awayday. [#2013naad](https://twitter.com/search?q=%232013naad&src=hash)


## Purpose
Look at how to use some of the powerful features of [SASS](http://sass-lang.com) to choreograph modular, maintainable and highly-flexible css keyframe animations. *Note: Using static CSS to choreograph css-animations is extremely tedious and bad for your health.*



## Demos
* Live demo: http://orbits.matthewcopeland.me
* Video: http://youtu.be/CI5oZjKps-w



## We'll be looking at..
* Touch on some SASS features.
* Bourbon - a SASS pattern library.
* CSS transforms (scale and rotate).
* CSS keyframe animations.
* CSS :nth-of-type.
* How to use the above to create the demo.



### SASS features
* [$variables](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#variables_) to drive our layouts and simplify tweaks/refactoring.
* [@mixins](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#mixins)
* [@for](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#id11) loops.
* [@function](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#function_directives)
* [darken() function](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#darken-instance_method)
* [Referencing Parent Selectors: &](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#referencing_parent_selectors_)


### Bourbon
We'll be using Bourbon, *a lightweight SASS pattern-library*, to support CSS3 vendor prefixes. This will clean-up our code a bit and make it more readable/maintainable.

An important note is that including bourbon doesn't write any code. It is merely a library of mixins that we can use if we so choose. *(aka not bootstrappy).*

[![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/bourbon-not-bootstrappopotamus.png)](https://twitter.com/matthewcopeland/status/282078621663887360)


#### Example use of bourbon

```scss
// scss

.foo {
  @include border-radius( 5px );
}
```


Outputs:

```css
/* css */

.foo {
  -webkit-border-radius: 5px;
     -moz-border-radius: 5px;
          border-radius: 5px;
}
```


***



### CSS Transforms

#### Scale
Scales an element based on its size.

```scss
.foo { transform: scale( 0.1 ); }

.bar { transform: scale( 2.3 ); }
```



***




#### Rotate
You can rotate an element around its X, Y and Z axes. There are a few ways to rotate an element.

* `rotate( deg )`
* `rotateX( deg )`
* `rotateY( deg )`
* `rotateZ( deg )`
* `rotate3d( x, y, z, deg )`


```scss
.foo { transform: rotate( 180deg ); } // default rotates z

.foo { transform: rotateZ( 180deg ); } // rotates Z

.foo { transform: rotateX( 180deg ); } // rotates X

.foo { transform: rotateY( 180deg ); } // rotates Y

```



##### Rotate3d
You gain improved-preformance from (some) webkit browsers by using `rotate3d`. See DeSandro's article in the [references](#references) below.

The syntax for `rotate3d` requires 4-arguments: X, Y, Z, and degrees to rotate.
```scss
.foo { transform: rotate3d( x, y, z, deg ) }
```

The axes' rotations are product of the degree-value and the axis-value.
```scss
.foo { transform: rotate3d( x*deg, y*deg, z*deg, deg ); }
```



##### Rotating the X-axis

The following will all rotate 180 degrees around around the X-axis.

```scss
.foo { transform: rotate( 180deg ); }

.foo { transform: rotateX( 180deg ); }

.foo { transform: rotate3d( 1, 0, 0, 180deg ); }

.foo { transform: rotate3d( .5, 0, 0, 360deg ); }

.foo { transform: rotate3d( 2, 0, 0, 90deg ); }
```



##### Rotating the Y-axis

The following will all rotate 180 degrees around around the Y-axis.

```scss
.foo { transform: rotateY( 180deg ); }

.foo { transform: rotate3d( 0, 1, 0, 180deg ); }

.foo { transform: rotate3d(  0, .5, 0, 360deg ); }

.foo { transform: rotate3d( 0, 2, 0, 90deg ); }
```



##### Rotating the Z-axis

The following will all rotate 180 degrees around around the Z-axis.

```scss
.foo { transform: rotateZ( 180deg ); }

.foo { transform: rotate3d( 0, 0, 1, 180deg ); }

.foo { transform: rotate3d(  0, 0, .5, 360deg ); }

.foo { transform: rotate3d( 0, 0, 2, 90deg ); }
```


***


### CSS Keyframe animations

#### Keyframes

This does not envoke an animation, but simply defines the keyframes/steps to animate between.

```scss
@-keyframes pulse {
  0%    { transform: scale(1); }
  100%  { transform: scale(2); }
}
```

#### Animation
Apply a set of keyframes to an element and tell it how long the animation will last.

```scss
.foo {
  animation-name: pulse;
  animation-duration: 3s;
}
```

```scss
.foo {
  animation: pulse 3s; // shorthand syntax
}
```

***


## Time to start building the milky way


### Set `background-color` using a variable and `darken()` function.

Set the body's `background-color` using a variable from our color palette and `darken()` function.

The `darken` and `lighten` functions allow you to move through the HSL color-space. This can be quite useful when need to create some contrast and already have a color-palette.

```scss
body {
  background: darken($blackblue, 10);
}
```

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/01-darken.png)

### Create a `#milkyway` container
We'll create a reusable `@mixin` to 'fill' the screen with the `#milkyway`. This will helpful later as we'll want to perform a zoom animation on everything inside the `#milkyway` later.


```scss
@mixin fill($position:fixed) {
  position: $position;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
```

```scss
#milkyway {
  @include fill;
}
```

*Note that this didn't change the appearance of the screen.*

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/01-darken.png)



## The Sun

### Variable-driven size and position

Define the `$sun-size`.

The `$sun-size` will come in handy when we need to align elements with our sun and/or base other elements on the `$sun-size`. We'll use this variable for `height`, `width`.


### Make a reusable `@mixin` for a circle
To create a circle, we'll need an object that is of equal height and width and has a 50% border-radius.


```scss
@mixin circle($size) {
  height: $size;
  width: $size;
  @include border-radius( 50% );
}
```

```scss
$sun-color: $lightorange;
$sun-size: 300px;

#sun {
  @include circle($sun-size);
  @include radial-gradient(50% 50%, circle closest-side, $sun-color, rgba($sun-color, 0.0) );
}
```


![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/02-sun.png)


### Center the sun

We also need to create a mixin to center the sun in the window. Since we have defined the size of the sun, we can set its `position`, `top`, `left`, `bottom` and `right` and `margin` properties.

We'll make 3 `@mixins` for this so that we can reuse pieces of it *(that'll come in later)*.

```scss
@mixin vertical-middle {
  top: 0;
  bottom: 0;
  margin-top: auto;
  margin-bottom: auto;
}

@mixin horizontal-center {
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
}

@mixin center {
  @include horizontal-center;
  @include vertical-middle;
}
```


```scss
$sun-color: $lightorange;
$sun-size: 300px;

#sun {
  position: fixed;
  @include center;
  @include circle($sun-size);
  @include radial-gradient(50% 50%, circle closest-side, $sun-color, rgba($sun-color, 0.0) );
}
```


![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/03-sun-center.png)



## Zoom-in animation
```scss
@include keyframes(zoomin) {
  from { @include transform( scale(0) ); }
  to { @include transform( scale(1) ); }
}
```

```scss
$zoomin-animation-delay: 0;
$zoomin-animation-duration: 4s;

#milkyway {
  @include fill;
  @include transform( scale(1) ); // sets inital scale and helps avoid flickering.
  @include animation( zoomin $zoomin-animation-duration $zoomin-animation-delay linear );
}
```

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/04-zoom-in-start.png)
![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/05-zoom-in-mid.png)
![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/06-zoom-in-75.png)
![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/07-zoom-in-end.png)



## Sun pulse animation

```scss
@include keyframes(pulse) {
  to { @include transform( scale(0.9) ); }
}
```

```scss
$pulse-animation-duration: 1.8s;

#sun {
  @include animation( pulse $pulse-animation-duration );
}
```


We want the sun to pulse, but we know that our use won't be able to see the animation until after the `#milkyway` is finished zooming in. So, we'll apply an `animation-delay` and make it equal to the `$zoomin-animation-duration`.


```scss
$pulse-animation-duration: 1.8s;
$pulse-animation-delay: $zoomin-animation-duration;

#sun {
  @include animation( pulse $pulse-animation-duration $pulse-animation-delay );
}
```

Once the pulse-animation begins, we want the animation to continue infinitely and to alternate the direction of the pulse.

```scss
$pulse-animation-delay: $zoomin-animation-duration;
$pulse-animation-duration: 1.8s;

#sun {
  @include animation( pulse $pulse-animation-duration $pulse-animation-delay alternate infinite linear );
}
```




## Orbits & Planets

### Orbit
Before we can make a planet, we need to make an orbit. Then we'll put the planet inside the orbit. This will let us animate the orbit and the planet will naturally move with its orbit.

* Base the `$orbit-size` on `$sun-size`.
* Reuse the circle `@mixin`.
* Reuse the center `@mixin`.

```scss
$orbit-size: $sun-size*1.2;

.orbit {
  position: fixed;
  @include center;
  border: 1px solid rgba(255,255,255, .2);
  @include circle($orbit-size);
}
```

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/08-orbit.png)



### Planet

* Base the `$planet-size` on `$sun-size`.
* Reuse the circle `@mixin`.
* Position the planet absolutely inside its orbit.
* Center the planet vertically using the verticle-middle `@mixin`.
* Place the planet directly over the orbit's border on the right side.


![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/09-planet.png)


### Create multiple orbits/planets

Use ruby/haml to quickly create multiple obits/planets.

```haml
#orbits
  - 9.times do
    .orbit
      .planet
```

* Use a `@for` loop to enlarge the size of each orbit.

```scss
.orbit {
  @for $i from 1 through $orbit-count {
    &:nth-of-type( #{$i} ) {
      @include circle( $orbit-size * (1 + .2*$i) ) );
    }
  }
}
```

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/10-multi-planet.png)


## Animate the orbits.

### Define the keyframes

#### Completing a 360 degree rotation
In order to create a complete 360-degree rotation, we have to guide the rotation through 3-steps. Usually, you would have to write this out, but here we'll use a `@for` loop.

* Define the value of your full `$rotation`.
* Define the number of steps to complete your rotation (`$rotation-step-count`).
* Calculate the value of a `$rotation-step`.


```scss
@include keyframes(orbit) {
  $rotation: 360;
  $rotation-step-count: 3;
  $rotation-step: $rotation/$rotation-step-count;

  @for $i from 1 through $rotation-step-count {
    #{$i * (100%/$rotation-step-count)} { @include transform( rotate3d(0,0,1, #{$i*$rotation-step}deg) ); }
  }
}
```

```css
/* css output of keyframes */

@-keyframes orbit {
  33.33333% { transform: rotate3d(0, 0, 1, 120deg); }

  66.66667% { transform: rotate3d(0, 0, 1, 240deg); }

  100%      { transform: rotate3d(0, 0, 1, 360deg); }
}
```

I don't really like the fact that my percentages don't come out clean. This may cause some hiccups in easing-calculations. Fortunately we used a loop, so we can easily change the `$rotation-step-count` from `3` to `4`.

```scss
@include keyframes(orbit) {
  $rotation: 360;
  $rotation-step-count: 4;
  $rotation-step: $rotation/$rotation-step-count;

  @for $i from 1 through $rotation-step-count {
    #{$i * (100%/$rotation-step-count)} { @include transform( rotate3d(0,0,1, #{$i*$rotation-step}deg) ); }
  }

  50% { opacity: .8; }
}
```

```css
/* css output from 4-step rotation */
@keyframes orbit {
  25%   { transform: rotate3d(0, 0, 1, 90deg); }

  50%   { transform: rotate3d(0, 0, 1, 180deg); }

  75%   { transform: rotate3d(0, 0, 1, 270deg); }

  100%  { transform: rotate3d(0, 0, 1, 360deg); }

  50% { opacity: .8; }
}
```

*Ah. Much cleaner.*




### Apply `orbit` keyframes to `.orbit`

We don't want the orbits to start until after the zoomin animation and a couple pulses of the sun.
So we'll set `$orbit-animation-delay` to reflect that.

```scss
$orbit-animation-delay: $pulse-animation-delay + $pulse-animation-duration*2;
$orbit-animation-duration: 3s;

.orbit {
  @include animation( orbit $orbit-animation-duration $orbit-animation-delay infinite linear );
}
```

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/11-orbiting.png)
![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/12-orbiting.png)
![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/13-orbiting.png)
![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/14-orbiting.png)




### Stagger the orbit animation
The current animation works, but it doesn't do much for me. I want to vary the speeds of the orbits. So we'll add some logic to multiply the `animation-duration` in the `.orbit` `@for` loop.


```scss
.orbit {
  @include animation( orbit $orbit-animation-duration $orbit-animation-delay infinite linear );


  @function nth-orbit($base, $i) {
    @return $base * (1 + .2*$i);
  }


  @for $i from 1 through $orbit-count {
    &:nth-of-type( #{$i} ) {
      @include circle( nth-orbit($orbit-size, $i) );
      @include animation-duration( nth-orbit($orbit-animation-duration, $i) );
    }
  }
}
```

![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/15-orbiting.png)
![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/16-orbiting.png)
![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/17-orbiting.png)
![ScreenShot](https://raw.github.com/matthewcopeland/orbits/master/screenshots/18-orbiting.png)

*Oh. That's better.*



***

## Subtitles
* Position the subtitles on the page.

### Display table and table-cell.

Vertically centering an unknown text-string with `display: table;` and `display: table-cell;` is nice.

Make the subtitle container a table and set the width.

```scss
#subtitles {
  display: table;
  width: 100%;    // tables aren't blocks. so you have to set the width.
  height: 100%;
  padding: 0 20px; // give it some breathing room on the edges.
  p {
    display: table-cell;
    vertical-align: middle;
  }
}
```

#### Tweak the last subtitle.
For the last subtitle, I want to do something a bit different. Note that as soon as we change the display property of the element, the rest of the table-cells fall into place.. beautiful.

Give the last subtitle some width boundaries and horizontally-center it. To get the vertical centering, we could do a few things. Here's a simple one: add a span in the subtitle and do another `table`/`table-cell`.  Any other ideas? Let's try them.




### Add the subtitle animation.
* Create the subtitle keyframes. For now we'll just fade them in and out.
* Create a variable for the sum of the animation time.
* Add some intial-lead time for the start.
* Devide that total-time by the number of messages.
* Delay each subtitle animation by the

```scss
$msg-count: 5;
$msg-lead-time: 2s;
$msg-time: ($total-animation-time + $msg-lead-time)/($msg-count);

@mixin subtitles {
  @for $i from 1 through $msg-count {
    &:nth-of-type(#{$i}) {
      @include animation-name(subtitles);
      @include animation-duration($msg-time);
      @include animation-delay( $msg-time * ($i - 1) );
    }
  }
}
```


We want to do some stuff to the 2nd-half of the subtitles and the last-subtitle. We could add this to the loop. Whether or not that is the best place for this logic, that's debatable. We'll go ahead and do that just to show and example of sass' `@if`.




## PLAY TIME!
Now that our animations are all lined up. It's time to have some fun. Change variables, mess with the orbit sizing function, add a planet-sizing function, etc.



## References

* Paul Irish on the benefits of animating with translate. http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft
* Lea Verou's animation's with one keyframe. http://lea.verou.me/2012/12/animations-with-one-keyframe
* David DeSandro on 3D transforms http://24ways.org/2010/intro-to-css-3d-transforms
* W3 http://www.w3.org/TR/css3-transforms
* Chris Coyier on `display: table; display: table-cell;` - http://css-tricks.com/centering-in-the-unknown
### Sass stuffs
* [Sass functions](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html)
* Bourbon http://bourbon.io

