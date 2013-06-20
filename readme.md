Orbits
=======

Demo for a stylesheet talk at 2013 ThoughtWorks North America Awayday.

## [Talk / full breakdown] http://matthewcopeland.me/blog/2013/06/10/orbits-choreographing-css-animations-with-sass

## Demos
* Live demo: http://orbits.matthewcopeland.me
* Video: http://youtu.be/CI5oZjKps-w


## Setup

This uses a lightweight sinatra wrapper, haml-server. https://github.com/bernerdschaefer/haml-server


Install the bundle

$`bundle install`


Start sass:

$`sass --watch site/stylesheets/sass/screen.scss:site/stylesheets/css/screen.css`


Start haml-server(sinatra):

$`haml-server site`
