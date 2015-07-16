# Shelf.js

[![Build Status](https://travis-ci.org/shakty/shelf.js.png?branch=master)](https://travis-ci.org/shakty/shelf.js)

Shelf.js is a unified api to write safely key-value pairs to a persistent storage either in the browser or in Node.js environment.

The api abstract from the actual storage medium, and gracefully degrades to the next one available.

## Technologies

Shelf.js is a mesh-up of `amplify.store` and the `cookies` library

 - http://amplifyjs.com/
 - http://code.google.com/p/cookies/


It combines the best of the two and adds some extra features in order to offer persistent storage capabilities in the browser.

Morever, if Douglas Crockford's  `JSON-js cycle.js` library is available, also cyclic objects can be serialized.

- https://github.com/douglascrockford/JSON-js

### amplify.store

amplify.store is a wrapper for various persistent client-side storage systems. amplify.store supports IE 5+, Firefox 2+, Safari 4+, Chrome, Opera 10.5+, iPhone 2+, Android 2+ and provides a consistent API to handle storage cross-browser.

amplify.store is meant to allow you to utilize all the latest storage technologies for those browsers that have them, while gracefully degrading for those without support.

### cookies library

This is a Javascript library for accessing and manipulating HTTP cookies in the web browser. You can get one or a list of cookies, set cookies, delete cookies, test if the browser accepts cookies. When JSON support is available, any JS value can be set to a cookie--it will be automatically serialized before being written to the cookie.

### file system support

Native file system writing and reading support is offered through Node.js (v.6 and v.8) fs api.

## Build

Create your customized build of Shelf.js  using the make file in the `bin` directory

```javascript
node make.js build // Standard build, about 7Kb minified
node make.js build -a -o shelf-full // full build, about 18Kb minified
node make.js build -l amplify,cookie // manually select libraries
```

### Help

```javascript
node make.js --help
```

## Usage

### Basic

```javascript

  // Store something on the first shelf available
  store('foo', {foo: 'bar'}, {});

  // Grab something from the shelf
  store('foo');
  // {foo: 'bar'}

  // Storing something on a specific shelf
  store.cookie(foo2, {foo2: 'bar2'});

```

### Checkings and configuration

```javascript

  // Check whether the browser offers persistent storage
  if (!store.isPersistent()) {
    alert('Browser storage and cookies are currently disabled');
  }

  // Check / set verbosity level
  store.verbosity = 1;

  // Check / set default shelf
  store.type = 'memory';

```

### On Quota Error

In modern browsers you can catch the error generated by exceeding the quota limit by overriding the method `store.onquotaerror`.

```javascript

   store.onquotaerror = function() {
    alert("Hey, your localStorage quota is finished!");
    // Clean up the mess code
  };

```

## License

[MIT](LICENSE)
