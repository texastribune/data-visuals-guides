# Text Editors

Three editors are used here at The Texas Tribune – [Atom](https://atom.io/), [Sublime Text 3](http://www.sublimetext.com/3) and [Visual Studio Code](https://code.visualstudio.com). We have no particular preference – try them all out! You're welcome to use anything else, too, but you'll be on your own.

### Atom

[Download the installer](https://atom.io/) and install as normal.

#### Hook Atom into your terminal

Atom does this automatically on install. You should be able to type `atom <path>` in your terminal to open files and folders with Atom.

#### Suggested reading

Check out the [Atom Flight Manual](https://atom.io/docs/v0.208.0/) – it's a good overview on how Atom works.

### Sublime Text 3

[Download the installer](http://www.sublimetext.com/3) and install as normal.

#### Wait, why version 3 instead of version 2?

> Sublime Text has an interesting release strategy – although `2` is the current version, `3` is the one everyone uses and a majority of plugins support now. Use `2` at your own peril.

#### Hook Sublime Text 3 into your terminal

Run the following in your terminal:

```sh
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl
```

Now you can type `subl <path>` in your terminal and Sublime will open that file or folder.

### Visual Studio Code

[Download the installer](https://code.visualstudio.com/docs/setup/mac) and install. Continue following the guide to set up shell access.