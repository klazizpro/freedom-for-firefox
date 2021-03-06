freedom-for-firefox
===================
A freedom.js distribution for inclusion in Firefox extensions.

# Installation
The freedom-for-firefox npm package contains a generated [javascript code module](https://developer.mozilla.org/en-US/docs/Mozilla/JavaScript_code_modules), freedom-for-firefox.jsm. This file can be included in your firefox
addon to interact with freedom.

`freedom-for-firefox.jsm` can be placed anywhere in your extension file structure. In the case of jetpack addons, you will likely want to place it somewhere in the data dir. To include it in jetpack addon, use:

```javascript
const {Cu} = require("chrome");
// Note: data.url is relative to your data directory
Cu.import(self.data.url("freedom-for-firefox.jsm"))
```

Or in classic firefox extensions use:

```javascript
Components.utils.import("freedom-for-firefox.jsm");
```

This will define the function `freedom` in the current scope, which behaves the same way as
freedom in any other context.

# Testing
`grunt test` will build an extension with jasmine integration tests and run the tests in Firefox.
You can extend this with your own tasks, by including this dependency in your own grunt project:

```javascript
grunt.loadNpmTasks('freedom-for-firefox');
```

You would then configure the `build-test-addon` task with your own jasmine tests, similarly to
how it is run by this project.

To view the browser console you will currently need to run firefox directly:
```bash
cd .build
../tmp/mozilla-addon-sdk/addon-sdk-1.17-official/bin/cfx run
```

# FAQ
- Mac OS X firewalls have been known to block WebRTC when set to its strictest setting.
  Be sure to allow an exception for Firefox for integration tests to pass

