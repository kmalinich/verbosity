# verbosity v0.0.16

![Project status](http://img.shields.io/badge/status-alpha-red.svg?style=flat) [![Build Status](http://img.shields.io/travis/MarkGriffiths/verbosity.svg?branch=master&style=flat)](https://travis-ci.org/MarkGriffiths/verbosity) [![Dependency Status](http://img.shields.io/david/MarkGriffiths/verbosity.svg?style=flat)](https://david-dm.org/MarkGriffiths/verbosity) [![devDependency Status](http://img.shields.io/david/dev/MarkGriffiths/verbosity.svg?style=flat)](https://david-dm.org/MarkGriffiths/verbosity#info=devDependencies) [![npm](https://img.shields.io/npm/v/@thebespokepixel/verbosity.svg?style=flat)](https://www.npmjs.com/package/@thebespokepixel/verbosity)

__Work in progress.__

## Install

```console
	npm install @thebespokepixel/verbosity --save
```

## Usage

Simple override the built in console object:

```js
	// This will duplicate the behaviour of the built in console object.
	
	console = require("@thebespokepixel/verbosity").console({
		out: process.stdout
		error: process.stderr
		verbosity: 5
	})

	/* 
	  This will direct all console output to stderr,
	  but silence 'info' and 'debug' messages.
	*/

	console = require("@thebespokepixel/verbosity").console({
		out: process.stderr
		verbosity: 3
	})


	// Or go mad with making up and number or custom console writers

	myUberConsole = require("@thebespokepixel/verbosity").console({
		out: myFancyWriteableStream
		verbosity: 5
	})
```

## API

The API inherits from Console, and all the argument parsing options are available.

### (critical | panic | emergency) args... (level 1)

Write a Critical/Emergency/Panic error message in red. Best used just before aborting the process with a `process.exit(1)`

```js
	console.panic('Core Flux Capacitor Meltdown!')
```

> <span style="background-color: black"> $ <span style="color: red; font-weight: bold"> CRITICAL: Core Flux Capacitor Meltdown!</span> </span> 

### error args... (level 1)

Write a normal error message in red.

```js
	console.error('This statement is false does not overload my logic circuits. moron.')
```

> <span style="background-color: black"> $ <span style="color: red"> ERROR:This statement is false does not overload my logic circuits. moron.</span> </span>

### warn args... (level 2)

Write a normal warning message in yellow.

```js
	console.warn("That tie doesn't go with that jacket.")
```

> <span style="background-color: black"> $ <span style="color: yellow"> That tie doesn't go with that jacket.</span> </span>

### log args... (level 3)

As console.log.

### info args... (level 4)

As console.info.

### debug args... (level 5)

Same and console.info, just a level lower.

### dir object [options]

As console.dir, but defaults to colour and zero depth.

### pretty object, depth

Pretty prints object, similar to OS X's plutil -p. Defaults to zero depth.

```js
	console.pretty(console)

	/* Yeilds:
		Object: VerbosityMatrix
		  critical ▸ [Function]
		  error ▸ [Function ▸ bound ]
		  warn ▸ [Function ▸ bound ]
		  log ▸ [Function ▸ bound ]
		  info ▸ [Function ▸ bound ]
		  debug ▸ [Function]
		  canWrite ▸ [Function]
		  ...
	*/
```

### yargs object, depth

Helper function for pretty printing a summary of the current 'yargs' options.

Only prints 'long options', `._` as 'arguments' and `$0` as 'self'.

```js
	console.yargs(yargs)

	/* Yeilds:
		Object (yargs):
		  left ▸ 2
		  right ▸ 2
		  mode ▸ 'hard'
		  encoding ▸ 'utf8'
		  ...
		  self ▸ '/usr/local/bin/truwrap'
	*/
```

### canWrite level

Returns true if a message of level would be printed.

```js
	if (console.canWrite(5)) {
		// Do something only if we're current logging at a debug level.
	}
```

### verbosity level

Set the current verbosity. The level will only stick if it's within the correct bounds. i.e 1-5.

### time

As console.time.

### timeEnd

As console.timeEnd.

### trace

As console.trace.

### assert

As console.assert.
