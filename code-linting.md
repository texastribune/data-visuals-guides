
#Code Linting Guide

Per [Wikipedia](http://en.wikipedia.org/wiki/Lint_(software)):

>In computer programming, lint was the name originally given to a particular program that flagged some suspicious and non-portable constructs (likely to be bugs) in C language source code. The term is now applied generically to tools that flag suspicious usage in software written in any computer language. The term lint-like behavior is sometimes applied to the process of flagging suspicious language usage. Lint-like tools generally perform static analysis of source code.

tl;dr Linters yell at you when you write bad code. They're more helpful than annoying, we promise.

##Atom

Execute the following in your terminal to install linting tools for Atom: `apm install atom-lint`. Alternativly, go the Atom package manager, search for `atom-lint`, and install the package. This will install lots of linting tools including jshint, flake8, and scsslint.

##Sublime Text 3

This tutorial involves alot of restarting Sublime, so ex out of all open Sublime windows and completely quit Sublime so it doesn't keep trying to open up your last opened window when you try to restart. It's also a good idea to start with a fresh terminal window free of running processes and virtual environments, so quit and restart terminal while you're at it.

Start by [installing the SublimeLinter package](http://sublimelinter.readthedocs.org/en/latest/installation.html#installing-via-pc): 

* **Step 1:** Quit Sublime (all the way, `cmd`+`q`) and open a brand new Sublime window. 
* **Step 2:** Hit 'cmd'+'shft'+'p' - this opens Sublime's Command Palatte which is basically a list of all of the supported add-ons for Sublime.
* **Step 3:** Type `install` and you should see `Package Control: Install Package` (this takes a minute- there are LOTS of packages) hit enter...
* **Step 4:** A list of available packages should show up, type `linter` and find `SublimeLinter`. Hit enter again.
* **Step 5:** It'll take a minute or two to install. Once it's finished, you'll see an install message in your text editor. Make sure it's not an error message and restart Sublime.

###`SublimeLinter-jshint`

Look for SiblimeLinter-jshint with `cmd`+`shft`+`p` and typing `jshint`

Hit enter to install. Wait for the install message, and restart Sublime.

This linter depends on some other packages being installed on your computer. Let's grab those- open your terminal and run `npm install jshint`.

Quit Sublime, and open a JavsScript file from one of your projects from the command line (run `subl <project path>`). If you don't see any yellow circles on the side or angry red boxes, open the command palatte and type `lint this view`. Run that and you should see at least a few lines of angry code.

### `SublimeLinter-flake8`

Flake8 is a python linter.

Start by going into your terminal and running `pip freeze` (make sure you're not in a virtual environment)

Followed by `pip install flake8`

Quit Sublime, and open a .py file. Like the jshint, you should see some yellow dots and boxes around things.

One thing that's slightly more important about Python than other languages is line length. This is to help your code be more readable and to prevent you from getting too crazy stringing things together. It's almost always better to break your code up into smaller, more managable chunks (this is also true for just about everything)

To help keep you honest, let's put some rulers in your `.py` files.

While you're still looking at your `.py` file, go up to the top bar and...

`Sublime Text` > `Preferences` > `Settings - More` > `Syntax Specific - User`

Copy + paste this snippet in there:

```py
{
  "rulers": [72, 79],
  "tab_size": 4
}
```
This should give you some sweet, naggy rules for all of your .py files.

###`Sublime​Linter-contrib-scss-lint`

Open your command palatte in Sublime and type `contrib-scss` and you should see `SublimeLinter-contrib-scss-lint`. Install it...

Back to your terminal (this one runs on Ruby so we'll have to do some Ruby things). Run `gem install scss-lint` followed by `rbenv rehash`.

Restart Sublime and restart your terminal. Open both back up and open an SCSS file from the terminal (`subl <path to scss file>`)

<!-- **Command Line**—You can also use these tools directly from the command line.

* **jshint**—To install [jshint](http://www.jshint.com/docs/) run `npm install jshint -g`. Whenever you want to lint your code, just run `jshint /path/to/file`. 
* **scss-lint**—To install [scss-lint](https://github.com/causes/scss-lint), run `gem install scss-lint`. Then run `scss-lint` on the folder or file you want to check.
* **flake8**—To install [flake8](https://flake8.readthedocs.org/en/2.1.0/), run `pip install flake8`. Then run `flake8` on the folder or file you want to check. -->