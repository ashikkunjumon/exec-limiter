
# exec-limiter

 [![Support me on Patreon][badge_patreon]][patreon] [![Buy me a book][badge_amazon]][amazon] [![PayPal][badge_paypal_donate]][paypal-donations] [![Travis](https://img.shields.io/travis/IonicaBizau/exec-limiter.svg)](https://travis-ci.org/IonicaBizau/exec-limiter/) [![Version](https://img.shields.io/npm/v/exec-limiter.svg)](https://www.npmjs.com/package/exec-limiter) [![Downloads](https://img.shields.io/npm/dt/exec-limiter.svg)](https://www.npmjs.com/package/exec-limiter)

> Limit the shell execution commands to <x> calls same time.

## :cloud: Installation

```sh
$ npm i --save exec-limiter
```


:bulb: **ProTip**: You can install the [cli version of this module](http://github.com/IonicaBizau/exec-limiter-cli) by running `npm i -g exec-limiter-cli`

## :clipboard: Example



```js
// Dependencies
var ExecLimiter = require("exec-limiter");

// Constants
const COMMAND = "sleep 5; date;";

// Create an instance of exec limiter
var el = new ExecLimiter(2);

// #1
el.add("sleep 5", function (err) {
    console.log(err || "Waited 5 seconds for the first time.");
});

// #2
el.add("sleep", ["7"], function (err) {
    console.log(err || "Waited another 7 seconds but probably I was ran in parallel with the other process.");
});

// #3
el.add("sleep 5", function (err) {
    console.log(err || "I was ran in parallel with the second process and finished fine.");
});

// #4
el.add("ls", ["-l"], { ignoreStdout: false }, function (err, stdout) {
    console.log(err || "The spawned 'ls -l' returned:\n" + stdout);
});

// These will be executed like below:
//
// Timeline: 0-1-2-3-4-5-6-7-8-9-10-11
//
//       #1: ==========
//       #2: ==============
//       #3:            ============
//       #4:               ==
//
// Notice how they run in parallel, but not more than 2 in the same time.
```

## :memo: Documentation


### `ExecLimiter(limit)`
Creates a new instance of `ExecLimiter`.

#### Params
- **Number** `limit`: The limit of commands to run same time.

#### Return
- **ExecLimiter** The `ExecLimiter` instance.

### `add(command, args, options, callback)`
Adds a new command to run in the buffer.

Usage:

```js
el.add(command, fn); // exec
el.add(command, args, fn); // spawn
el.add(command, options, fn); // exec
el.add(command, args, options, fn); // spawn
```

#### Params
- **String** `command`: The command to run as string.
- **Object** `args`: The command arguments as array of strings (optional).
- **Object** `options`: The options passed to the spawn/exec function, but extended with the following fields:
 - `ignoreStdout` (Boolean): If `false`, then the stdout output will be stored ant called back.
- **Function** `callback`: The callback function.

#### Return
- **ExecLimiter** The `ExecLimiter` instance.



## :yum: How to contribute
Have an idea? Found a bug? See [how to contribute][contributing].


## :sparkling_heart: Support my projects

I open-source almost everything I can, and I try to reply everyone needing help using these projects. Obviously,
this takes time. You can integrate and use these projects in your applications *for free*! You can even change the source code and redistribute (even resell it).

However, if you get some profit from this or just want to encourage me to continue creating stuff, there are few ways you can do it:

 - Starring and sharing the projects you like :rocket:
 - [![PayPal][badge_paypal]][paypal-donations]—You can make one-time donations via PayPal. I'll probably buy a ~~coffee~~ tea. :tea:
 - [![Support me on Patreon][badge_patreon]][patreon]—Set up a recurring monthly donation and you will get interesting news about what I'm doing (things that I don't share with everyone).
 - **Bitcoin**—You can send me bitcoins at this address (or scanning the code below): `1P9BRsmazNQcuyTxEqveUsnf5CERdq35V6`

    ![](https://i.imgur.com/z6OQI95.png)

Thanks! :heart:


## :dizzy: Where is this library used?
If you are using this library in one of your projects, add it in this list. :sparkles:


 - [`engine-tools`](https://github.com/jillix/engine-tools) (by jillix)—Engine Tools library and CLI app.
 - [`exec-limiter-cli`](https://github.com/IonicaBizau/exec-limiter-cli#readme)—Run multiple shell commands in parallel, but with a limit.
 - [`git-stat`](https://github.com/maxdeviant/git-stat#readme) (by Marshall Bowers)—Statistic generation for Git.
 - [`gpm`](https://github.com/IonicaBizau/gpm)—npm + git = gpm - Install NPM packages and dependencies from git repositories.
 - [`gry`](https://github.com/IonicaBizau/node-gry)—A minimalist NodeJS wrapper for the `git` commands. `gry` stands for the Git RepositorY.
 - [`npmreserve`](https://github.com/IonicaBizau/npmreserve)—Reserve package names on NPM.

## :scroll: License

[MIT][license] © [Ionică Bizău][website]

[badge_patreon]: http://ionicabizau.github.io/badges/patreon.svg
[badge_amazon]: http://ionicabizau.github.io/badges/amazon.svg
[badge_paypal]: http://ionicabizau.github.io/badges/paypal.svg
[badge_paypal_donate]: http://ionicabizau.github.io/badges/paypal_donate.svg
[patreon]: https://www.patreon.com/ionicabizau
[amazon]: http://amzn.eu/hRo9sIZ
[paypal-donations]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=RVXDDLKKLQRJW
[donate-now]: http://i.imgur.com/6cMbHOC.png

[license]: http://showalicense.com/?fullname=Ionic%C4%83%20Biz%C4%83u%20%3Cbizauionica%40gmail.com%3E%20(https%3A%2F%2Fionicabizau.net)&year=2015#license-mit
[website]: https://ionicabizau.net
[contributing]: /CONTRIBUTING.md
[docs]: /DOCUMENTATION.md
