glance.js
==

[![Build Status](https://travis-ci.org/jarofghosts/glance.png?branch=master)](https://travis-ci.org/jarofghosts/glance)

Glance provides a quick disposable http server for static files

## installation

``
npm install -g glance
``

## usage

Run `glance` from within a directory and you are immediately serving the files from within that directory

Alternatiely, you can `require('glance')` and use it as a module within your own code.
The glance module provides access to the Glance object as well as `createGlance`, a factory method.

Some sample code might just look something like this:

````js
var glance = require('glance'),
// init a glance object with custom options (all totally optional)
    g = createGlance({
      dir: '../Files', // defaults to current working dir
      port: 86753, // defaults to 61403
      verbose: true // defaults to false
    });

// start the server
g.start();

// listen for read events
g.on('read', function (req) {
  console.dir(req);
  /* req object of format:
     { fullPath: 'requested path',
       ip: 'remote ip address',
       method: 'requested method',
       response: 'response object' }
  */
});

// listen for error events
g.on('error', function (req) {
  console.log('BAD!!!!');
  // stop the glance server
  g.stop();
});
````

## options

`glance`
+ `-d [dir]` serve a different directory than the current working directory
+ `-h` print help screen with option listing
+ `-p [port]` open server a different port than 61403
+ `-V` print version information
+ `-v` enable verbose mode, printing log to stdout. Off by default

## license

MIT
