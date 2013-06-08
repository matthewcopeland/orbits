Talk for Awayday
===================

Demo for a stylesheet talk at 2013 ThoughtWorks North America Awayday. [#2013naad](https://twitter.com/search?q=%232013naad&src=hash)

## Our goal

### Live demo: http://orbits.matthewcopeland.me
### Video: http://youtu.be/CI5oZjKps-w


## What we'll be learing about
* Some Sass features
* CSS Keyframe animations



### Sass features
Our goal *(a highly flexible, modular and maintainable animation)* would extremely tedious with static css. To give us what we want, we'll be utilizing [Sass](http://sass-lang.com).

Some of the key features of sass that we'll be using today:

* [@for](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#id11) loops.
* [@mixin](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#mixins)s
* [$variables](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#variables_) to drive our layouts and simplify tweaks/refactoring.
* [@function](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#function_directives)
* [rgba() sass function](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#rgba-instance_method)
* [darken() sass function](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#darken-instance_method)

### Bourbon
A lightweight sass-library to support css3 vendor prefixes. This allows your code to be much cleaner and more readable.

#### Example

```scss
.foo {
  @include border-radius( 5px );
}
```


Outputs:

```css
.foo {
  -webkit-border-radius: 5px;
     -moz-border-radius: 5px;
          border-radius: 5px;
}
```




### CSS Keyframe animations

#### Keyframes

This does not envoke an animation, but simply defines the keyframes/steps to animate between.

```scss
//example
@-keyframes foo {
  0% { opacity: 0; }
  100% { opacity: 1; }
}
```

#### Animation
Apply a set of keyframes to an element and tell it how long the animation will last.

```scss
//example implementing the foo keyframes from above

.bar {
  animation-name: foo;
  animation-duration: 3s;
}


// or shorthand

.bar {
  animation: foo 3s;
}
```



## Milky-way

### Variables and the `darken()` function
The milky-way utilzes a variable from our color palette and `darken()` function. The `darken` and `lighten` functions allow you to move through the HSL color-space. This can be quite useful when you want to stay consistent within your color-palette and need to create some contrast.  You'll see this become more useful in the Earth.



## The Sun

### Variable-driven size and position

Define the `$sun-size`.

The `$sun-size` will come in handy when we need to align elements with our sun and/or base other elements on the `$sun-size`. We'll use this variable for `height`, `width`.


### Make a utility for a Circle
To create a circle, we'll need an object that is of equal height and width and has a 50% border-radius.

```scss
@mixin circle($size) {
  height: $size;
  width: $size;
  @include border-radius( 50% );
}
```

### Center the sun.
To center the element, I've made a `@mixin`.


### Animate the sun
* Setup the pulse keyframes and apply them to the sun.
* Setup the zoom-in/out keyframes and apply them to the milky-way.


## Orbits & Planets

### Orbit
Before we can make a planet, we need to make an orbit. Then we'll put the planet inside the orbit. This will let us animate the orbit and the planet will naturally stay

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


### The orbit/planet animation.

The orbit is what we'll be rotating around the sun. By rotating the orbit, the planet will move with it.

* Count the number of orbits/planets.




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

### CSS stuff
* Paul Irish on the benefits of animating with translate. http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft
* Lea Verou's animation's with one keyframe. http://lea.verou.me/2012/12/animations-with-one-keyframe
* David DeSandro on 3D transforms http://24ways.org/2010/intro-to-css-3d-transforms
* W3 http://www.w3.org/TR/css3-transforms
* Chris Coyier on `display: table; display: table-cell;` - http://css-tricks.com/centering-in-the-unknown
### Sass stuffs
* [Sass functions](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html)
* Bourbon http://bourbon.io

## Feedback
* A page on what sass and bourbon do.
