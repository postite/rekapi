# Rekapi - Keyframes for JavaScript

Rekapi is a keyframe animation library for JavaScript.  It gives you:

* A keyframe-based Model by which to structure an animation
* APIs to control the playback of an animation

Rekapi does not define drawing methods.  Rendering is abstract, and the library
exposes a common interface for defining rendering methods.

Rekapi has two dependencies:
[Underscore](https://github.com/documentcloud/underscore) and
[Shifty](https://github.com/jeremyckahn/shifty).

Rekapi has been tested in and supports:

  * Modern HTML5 browsers
  * IE 7/8 (9 probably works; has not been tested)
  * Node.js

If you have any questions at all about Rekapi, please post them to the [Google
Group](https://groups.google.com/forum/?fromgroups#!forum/rekapi).  Also, check
out the [Getting Started Guide
](https://github.com/jeremyckahn/rekapi/blob/master/docs/getting_started.md).

Please note:  Rekapi is a rewrite of
[Kapi](https://github.com/jeremyckahn/kapi). Rekapi is very similar to Kapi,
but they are not identical.  Rekapi is not a drop-in replacement for Kapi.
Rekapi is way better, so you should use it instead.

The API may change somewhat before reaching 1.0.  __[See how to upgrade from
older versions.
](https://github.com/jeremyckahn/rekapi/blob/master/docs/upgrading.md)__.

## What is keyframing?

Keyframing is an animation technique for defining states at specific points in
time. Animations are always rendered as frames to the screen, and keyframing
allows you to define the key points at which the motion in the animation
changes - all of the frames that exist between those points are interpolated
for you.  It is a powerful way to construct a complex animation.

## How do I use Rekapi?

You can think of a Rekapi animation as a Model with Views, complimented by APIs
to control the playback. Its usage boils down to four steps:

* Define some `Kapi.Actor`s
* Instantiate and add the Views to a `Kapi` instance
* Define keyframes (states) for the `Kapi.Actor`s
* Play the animation

## Model - Kapi

The Model maintains the state of an animation.  Rekapi's Model is represented
by the `Kapi` Object.  The Model controls the state of the animation and
renders the Views.

## View - Kapi.Actor

The Actors are the individual components of an animation.  If you want to move
a circle from left to right in your animation, that circle is an Actor.  If you
want to add a square to your animation that moves up and down, that square is
another, separate actor.  Actors are represented by the `Kapi.Actor` Object and
its subclasses.

## Control APIs

There are animation control methods built into the `Kapi` Object.  These
methods include `play()`, `pause()` and `stop()`.

## Contexts

Rekapi works by passing data from a Model to a View.  The View then renders the
data based on a context.  Rekapi treats contexts generically, and you can
create more as you need them.  Currently, the standard Rekapi build includes
rendering contexts for the DOM and `<canvas>`.

A Rekapi context does two things: It extends the prototype of the `Kapi`
Object, and it subclasses `Kapi.Actor`.  This is how Rekapi renders to the
`<canvas>` and DOM: The Canvas and DOM renderers create `Kapi.CanvasActor` and
`Kapi.DOMActor`, respectively.

The `Kapi.Actor` base class only renders raw data, it doesn't render data
visually because it doesn't have a context.  Use `Kapi.DOMActor` and
`Kapi.CanvasActor` to render to the screen.

## AMD

You can optionally load Rekapi as an
[AMD](https://github.com/amdjs/amdjs-api/wiki/AMD) module by using a loader
such as [RequireJS](http://requirejs.org). This has the added benefit of not
creating a global `Kapi` variable.

Caution: You can only require `rekapi.js` or `rekapi.min.js` as AMD modules. It
will not work with `rekapi-underscore-shifty.min.js`.

Here is an example of how you can use it with RequireJS:

````javascript
// This example assumes that there is a `lib` directory in your project
require.config({
  paths: {
    shifty: "lib/shifty",
    underscore: "lib/underscore.min",
    rekapi: "lib/rekapi"
  }
});

// Dependencies (Underscore and Shifty) are automatically loaded.
require(['rekapi'], function(Kapi) {
  var kapi = new Kapi();
});
````

## Node

Rekapi can be used in Node.js.  This can be useful for generating keyframe
data.  Usage is the same as in the browser.  Loading the code requires the
[r.js](https://github.com/jrburke/r.js/blob/master/dist/r.js) script and looks
a lot ike the AMD approach above:

````javascript
var requirejs = require('requirejs');
requirejs.config({
  paths: {
    shifty: "dist/shifty.min",
    underscore: "dist/underscore-min",
    rekapi: "dist/rekapi"
  }
});

requirejs(['rekapi'], function(Kapi) {
  var kapi = new Kapi();
});
````

## Contributors

  * [Franck Lecollinet](https://github.com/sork)
