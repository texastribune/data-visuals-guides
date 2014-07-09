
#Code Linting Guide

Per [Wikipedia](http://en.wikipedia.org/wiki/Lint_(software)):

>In computer programming, lint was the name originally given to a particular program that flagged some suspicious and non-portable constructs (likely to be bugs) in C language source code. The term is now applied generically to tools that flag suspicious usage in software written in any computer language. The term lint-like behavior is sometimes applied to the process of flagging suspicious language usage. Lint-like tools generally perform static analysis of source code.

###Installation

**Atom**—Execute the following in your terminal to install linting tools for Atom: `apm install atom-lint`. Alternativly, go the Atom package manager, search for `atom-lint`, and install the package. This will install lots of linting tools including jshint, flake8, and scsslint.

**Sublime Text 3**—Start by [installing the SublimeLinter package](http://sublimelinter.readthedocs.org/en/latest/installation.html#installing-via-pc). Then install the following additional packages:

* `SublimeLinter-jshint`
* `SublimeLinter-flake8`
* `Sublime​Linter-contrib-scss-lint`


	This requires you to have the Sublime package manager installed.

**Command Line**—You can also use these tools directly from the command line.

* **jshint**—To install [jshint](http://www.jshint.com/docs/) run `npm install jshint -g`. Whenever you want to lint your code, just run `jshint /path/to/file`. 
* **scss-lint**—To install [scss-lint](https://github.com/causes/scss-lint), run `gem install scss-lint`. Then run `scss-lint` on the folder or file you want to check.
* **flake8**—To install [flake8](https://flake8.readthedocs.org/en/2.1.0/), run `pip install flake8`. Then run `flake8` on the folder or file you want to check.