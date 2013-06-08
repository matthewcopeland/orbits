Orbits talk
=============

A stylesheet talk at 2013 ThoughtWorks North America Awayday. [#2013naad](https://twitter.com/search?q=%232013naad&src=hash)


## Purpose
Look at how to use some of the powerful features of [SASS](http://sass-lang.com) to choreograph modular, maintainable and highly-flexible css keyframe animations. *A task that would extremely tedious with static css.*



## Demos
* Live demo: http://orbits.matthewcopeland.me
* Video: http://youtu.be/CI5oZjKps-w



## We'll be looking at..
* Touch on some SASS features.
* Bourbon - a SASS pattern library.
* CSS transforms (scale and rotate).
* CSS keyframe animations.
* How to use the above to create the demo.



### SASS features
* [$variables](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#variables_) to drive our layouts and simplify tweaks/refactoring.
* [@mixins](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#mixins)
* [@for](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#id11) loops.
* [@function](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#function_directives)
* [darken() function](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#darken-instance_method)


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
.foo {
  transform: scale( 0.1 );
}

.bar {
  transform: scale( 2.3 );
}
```



***




#### Rotate
You can rotate an element around its X, Y and Z axes. There are a few ways to rotate an element.

* rotate( deg )
* rotateX( deg )
* rotateY( deg )
* rotateZ( deg )
* rotate3d( x, y, z, deg )


```scss
.foo { transform: rotate( 180deg ); } // default rotates X

.foo { transform: rotateX( 180deg ); } // rotates X

.foo { transform: rotateY( 180deg ); } // rotates Y

.foo { transform: rotateZ( 180deg ); } // rotates Z
```



##### Rotate3d
You gain improved-preformance from (some) webkit browsers by using `rotate3d`. See DeSandro's article in the [references](#references) below.

The syntax for `rotate3d` requires 4-arguments: X, Y, Z, and degrees to rotate.
```scss
.foo {
  transform: rotate3d( x, y, z, deg )
}
```

The axes' rotations are product of the degree-value and the axis-value.
```scss
.foo {
  transform: rotate3d( x, y, z, deg )
}
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
  0% { transform: scale(1); }
  100% { transform: scale(2); }
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


##### Shorthand animation syntax

```scss
.bar {
  animation: foo 3s; // shorthand syntax
}
```



## Time to start building


### Variable-driven colors and the `darken` function

Set the body's `background-color` using a variable from our color palette and `darken()` function.

The `darken` and `lighten` functions allow you to move through the HSL color-space. This can be quite useful when need to create some contrast and already have a color-palette.



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

### Create a mixin to center the sun in the window


### Animate the sun
* Setup the pulse keyframes and apply them to the sun.
* Setup the zoom-in/out keyframes and apply them to the milky-way.


## Orbits & Planets

### Orbit
Before we can make a planet, we need to make an orbit. Then we'll put the planet inside the orbit. This will let us animate the orbit and the planet will naturally move with its orbit.

* Base the `$orbit-size` on `$sun-size`.
* Reuse the circle `@mixin`.
* Reuse the center `@mixin`.
* Fix the orbit to be centered in the window.

### Planet

* Base the `$planet-size` on `$sun-size`.
* Reuse the circle `@mixin`.
* Position the planet absolutely inside its orbit.
* Center the planet vertically using the verticle-middle `@mixin`.
* Place the planet directly over the orbit's border on the right side.


### Create multiple orbits/planets

* Use ruby to quickly create multiple obits/planets.
* Use a `@for` loop to enlarge the size of each orbit and position it.
* Create the sizing-loop to make the process easier.
* Animate the orbits.



## Animation timing
* Setup variables for the animation's arguments.
* Hook the animations together in the variables file.
* Use the sum total of previous animation to determine when to execute the next animation.


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

