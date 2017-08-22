# Timer 2.0 Library for Corona SDK

```
Copyright (c) 2015-2017 Jason Schroeder
http://www.jasonschroeder.com
http://www.twitter.com/schroederapps
```

This Lua module for Corona SDK overwrites the "stock" timer library with new functions that add the ability to pause/resume/cancel all active timers at once, or to pause/resume/cancel a subset of active timers by tagging them, similar to what Corona Labs did with their transition library back in 2015.

## How To Use The Timer 2.0 Library

Updating the timer library to “timer 2.0” in your Corona project is as simple as these two steps:

* Download timer2.lua and place it in your project’s root directory.
* Require the library in your project by adding this one line of code, preferably near the top of your main.lua:
  `require("timer2")`

By taking those steps, you have updated Corona’s built-in timer library to version 2.0. Note that your existing code will continue to work – version 2.0 is fully backwards-compatible with the current official timer APIs. But you also gain access to these new features:

* **timer.performWithDelay()** now accepts two new optional function arguments: tag and exclude:
  * **tag** is a string that appends a tag to the created timer that can be used to pause, resume, or cancel all timers with the same tag at once. Defaults to nil.
  * **exclude** is a boolean (true/false) parameter that, when set to true, excludes the timer from being impacted by timer.pause(), timer.resume(), or timer.cancel() calls that do not specifically target it by passing the timer’s handle or tag. Timers that are mission-critical and should always run should have their exclude parameter set to true. Defaults to false.

  These new arguments can be added in any order to the end of any existing timer.performWithDelay() call. As an example, the following code would create a timer with the tag “myTag” that is excluded from non-specific pause, resume, or cancel calls: `timer.performWithDelay(1000, myFunction, 1, "myTag", true)`

* **timer.pause(), timer.resume(), and timer.cancel()** still work as before, but with the following new features:
  * You can pause, resume, or cancel all active timers (unless they have their exclude parameter set to true) by calling timer.pause(), timer.resume(), or timer.cancel() with no arguments.
  * You can pause, resume, or cancel all timers with a specific tag by passing the tag as a parameter. For example, the following code would pause all active timers with the tag “myTag”: `timer.pause("myTag")`
