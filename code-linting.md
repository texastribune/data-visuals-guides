# Code Linting Guide

Per [Wikipedia](http://en.wikipedia.org/wiki/Lint_(software)):

> In computer programming, lint was the name originally given to a particular program that flagged some suspicious and non-portable constructs (likely to be bugs) in C language source code. The term is now applied generically to tools that flag suspicious usage in software written in any computer language. The term lint-like behavior is sometimes applied to the process of flagging suspicious language usage. Lint-like tools generally perform static analysis of source code.

tl;dr &mdash; Linters tell you when you write suboptimal code. They're helpful!

## Sublime Text 3

This tutorial will require you to restart Sublime Text 3 multiple times &mdash; go ahead and close all open Sublime Text windows completely with CMD + Q. It's also a good idea to start with a fresh Terminal window.

### Package Control

This guide also assumes you've installed [Package Control](https://packagecontrol.io/installation). This makes it possible to install plugins. To open Package Control's installer, press `CMD` + `SHIFT` + `P` to open Sublime Text's Command Palette, then search for `Package Control: Install Package`. We'll be making all our selections in this list.

### SublimeLinter

First, we'll install [SublimeLinter](http://www.sublimelinter.com/en/latest/).

Navigate to Package Control's installer and search for `SublimeLinter`. A long list of available packages will show up &mdash; we're looking for the one just named `SublimeLinter`. Highlight it and hit enter.

It'll take a few seconds. Once it's finished, you'll see an install message. Make sure it's not an error message, then restart Sublime Text.

### SublimeLinter-jshint

> `jshint` depends on Node.js &mdash; make sure it's installed and working.

[JSHint](http://jshint.com/) a JavaScript linter. It'll call you out for things like misplaced double quotes and other syntax errors.

Look for `SublimeLinter-jshint` in Package Control's install list, highlight it, then hit enter to install. Wait for the install message then restart Sublime Text.

`SublimeLinter-jshint` depends on the Node.js package [`jshint`](https://github.com/jshint/jshint). We need to install it in our terminal so SublimeLinter can use it.

To install it, run the following:

```sh
npm install -g jshint
```

Quit and restart Sublime Text, and then open a JavsScript file from one of your projects from the command line with the `subl` command. You should see some red or yellow errors (unless you're really good).

### SublimeLinter-flake8

> `flake8` depends on Python &mdash; make sure it's installed and working.

[Flake8](https://flake8.readthedocs.org/en/2.3.0/) is a Python linter. It's a wrapper around PyFlakes, pep8 and Ned Batchelder’s McCabe script. It'll call out things like trailing white space and declaring variables or functions that are never used. It'll also point out when your functions get too complex and should be broken into smaller pieces.

First, find `SublimeLinter-flake8` via Package Control's install, highlight it, then hit enter. Wait for the install message and restart Sublime Text.

It's important to not be in a virtual environment for this next step! If you aren't sure, open a brand new Terminal window.

Then run:

```sh
pip install flake8
```

### Sublime​Linter-contrib-scss-lint

> `scss-lint` depends on Ruby &mdash; make sure it's installed and working.

[scss-lint](https://github.com/brigade/scss-lint) is a SCSS linter. It'll point out things like forgetting to put a space between your class name and the bracket, or when you forget to alphabetize attributes.

Search for `SublimeLinter-contrib-scss-lint` in Package Control's installer, highlight it, and hit enter.

In your terminal, we need to install the Ruby gem `scss-lint` so SublimeLinter can use it.

```sh
gem install scss_lint
```

Restart Sublime and restart your terminal. Now `.scss` files should show errors.

### SublimeLinter-json

This package adds linting for `.json` files. Luckily the linter is built in to Sublime Text, so no extra installs are needed.

Just install `SublimeLinter-json` via the Package Control installer, restart Sublime Text, and you're good to go.

## Atom

TK
