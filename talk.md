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


### Make a utility for a Circle
In this utility, we'll need to include a few things: `height`, `width`.

```scss
@mixin circle($size) {
  display: block;
  height: $size;
  width: $size;
  @include border-radius($size/2);
}
```


### Animate the sun
* Setup a mixin for the sun animation.
*


## Orbits & Planets
Before we can make a planet, we need to make an orbit.

* Base the `$orbit-size` on `$sun-size`.
* Center the orbits.
* Add the planet.
* Give the planet a default position.



### The orbit/planet animation.
The orbit is what we'll be rotating around the sun. By rotating the orbit, the planet will move with it.
* Count the number of orbits/planets.
* Create the sizing-loop to make the process easier.



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
* Now that our animations are all lined up. It's time to have some fun. Change variables, mess with the orbit sizing function, add a planet-sizing function, etc.



## References

### CSS stuff
* Paul Irish on the benefits of animating with translate. http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft
* Lea Verou's animation's with one keyframe. http://lea.verou.me/2012/12/animations-with-one-keyframe
* David DeSandro on 3D transforms http://24ways.org/2010/intro-to-css-3d-transforms
* W3 http://www.w3.org/TR/css3-transforms
* Bourbon http://bourbon.io
