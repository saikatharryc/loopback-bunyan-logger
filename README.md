# loopback-bunyan-logger
updated   {loopback-component-logger}
 
 **incase if you dont want the child node logs. please use the version ^1.1.2
 
Logging component for [loopback] using [bunyan] logger with additional loopback specific hooks and log management API

[![NPM](https://nodei.co/npm/loopback-bunyan-logger.png?downloads=true)](https://nodei.co/npm/loopback-bunyan-logger/) [![NPM](https://nodei.co/npm-dl/loopback-bunyan-logger.png?months=1&height=2)](https://nodei.co/npm/loopback-bunyan-logger/)


[![Build Status](https://travis-ci.org/saikatharryc/loopback-bunyan-logger.svg?branch=master)](https://travis-ci.org/saikatharryc/loopback-bunyan-logger)


# Features

- Default logger using [bunyan]
- Can use of custom bunyan [streams] to create root logger
- Hook: Basic performance instrumentation for remote execution
- Hook: Log management API (configurable)

# Usage

Example _server.js_:

```js
var loopback = require('loopback');
var boot = require('loopback-boot');
var rootlogger = bunyan.createlogger({name: 'myloopbackAPI'});
var logger = require('loopback-bunyan-logger')(rootlogger);
var app = module.exports = loopback();

```

If rootlogger is not provide, the component creates a logger with default
 [bunyan] settings:

```js
var loopback = require('loopback');
var boot = require('loopback-boot');
var logger = require('loopback-bunyan-logger')();
var app = module.exports = loopback();

```

Child loggers can be created for model as shown below. By default child loggers
inherit the log level from root.

```js

var logger = require('loopback-bunyan-logger')('TestModel');
module.exports = function(TestModel) {
    logger.debug('Initializing TestModel');
};

```

To add hooks and log management API to [loopback], add configuration to component-config.json:

```js
{
  "loopback-component-explorer": {
    "mountPath": "/explorer"
  },
  "loopback-bunyan-logger": {
      "enableAPI" : true
  }
}

```
Make sure enableHttpContext is set as true in config.json for to allow collection
 of datasources performance within req/res
If you dont want expand the child nodes please use version @1.1.2
# License

[GNU](https://github.com/saikatharryc/loopback-bunyan-logger/blob/master/LICENSE)
 
# Create Issue
  Create issue here [here](https://github.com/saikatharryc/loopback-bunyan-logger/issues)

# Roadmap
- Additional Unit Test and Coverage
- Integrate with Strongloop Devops tools

# Known Issue
- datasources performance will not recorded at times when loopback context is null. Noticed this issue when a composite called MongoDB followed by REST. Only MongoDB response time was recorded and REST was missing.

# See Also

- [Loopback][loopback]
- [bunyan][bunyan]

[bunyan]: https://github.com/trentm/node-bunyan
[loopback]: http://loopback.io
[streams]: https://github.com/trentm/node-bunyan#streams
