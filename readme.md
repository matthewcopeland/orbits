Orbits
=======

Demo for a stylesheet talk at 2013 ThoughtWorks North America Awayday.

For the working talk, checkout [talk.md](https://github.com/matthewcopeland/orbits/blob/master/talk.md).


## Setup

This uses a lightweight sinatra wrapper, haml-server. https://github.com/bernerdschaefer/haml-server


Install the bundle

$`bundle install`


Start sass:

$`sass --watch site/stylesheets/sass/screen.scss:site/stylesheets/css/screen.css`


Start haml-server(sinatra):

$`haml-server site`
