<!---------------------------------------------------------------------------->
<!-- STOP, LOOK & LISTEN!                                                   -->
<!-- ====================                                                   -->
<!-- Do NOT edit this file directly since it's generated from a template    -->
<!-- file, using https://github.com/IonicaBizau/node-blah                   -->
<!--                                                                        -->
<!-- If you found a typo in documentation, fix it in the source files       -->
<!-- (`lib/*.js`) and make a pull request.                                  -->
<!--                                                                        -->
<!-- If you have any other ideas, open an issue.                            -->
<!--                                                                        -->
<!-- Please consider reading the contribution steps (CONTRIBUTING.md).      -->
<!-- * * * Thanks! * * *                                                    -->
<!---------------------------------------------------------------------------->

# exec-limiter [![Donate now][donate-now]][paypal-donations]

Limit the shell execution commands to <x> calls same time.

## Installation

```sh
$ npm i exec-limiter
```

## Example

```js
// Dependencies
var ExecLimiter = require("exec-limiter");

// Constants
const COMMAND = "sleep 5; date;";

// Create an instance of exec limiter
var el = new ExecLimiter(10)
  , i = 0
  , c = 0
  ;

// Exec the command 30 times, but not more than 10 same time
for (; i < 30; ++i) {
    el.add(COMMAND, function (err, stdout) {
        console.log((++c) + "> " + stdout);
    });
}

```

## Documentation

### `ExecLimiter(limit)`
Creates a new instance of `ExecLimiter`.

#### Params
- **Number** `limit`: The limit of commands to run same time.

#### Return
- **ExecLimiter** The `ExecLimiter` instance.

### `add(command, options, callback)`
Adds a new command to run in the buffer.

#### Params
- **String** `command`: The command to run.
- **Object** `options`: The options to pass to the exec function.
- **Function** `callback`: The callback function.

#### Return
- **ExecLimiter** The `ExecLimiter` instance.

## How to contribute
Have an idea? Found a bug? See [how to contribute][contributing].

## License
[KINDLY][license] © [Ionică Bizău][website]–The [LICENSE](/LICENSE) file contains
a copy of the license.

[license]: http://ionicabizau.github.io/kindly-license/?author=Ionic%C4%83%20Biz%C4%83u%20%3Cbizauionica@gmail.com%3E&year=2015
[contributing]: /CONTRIBUTING.md
[website]: http://ionicabizau.net
[docs]: /DOCUMENTATION.md
[paypal-donations]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MG98D7NPFZ3MG
[donate-now]: http://i.imgur.com/jioicaN.png