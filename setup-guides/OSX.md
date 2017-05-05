# Setting up your Mac

### Make sure you're the admin

Everything we do here is only going to work if you have admin privileges. How do you know if you have it?

1. Open your `System Preferences`.
2. Click on `Users & Groups`.
3. Do you see your name with `Admin` written below it on the left? Awesome! You're the admin.

![Are you the admin?](http://i.imgur.com/rTsdp5C.png?1)

Don't have admin powers? Reach out to [Rodney](rgibbs@texastribune.org) and he'll get you set up.

### Check for OSX updates

If your computer is brand new, you may have a few outstanding operating system updates. Make sure to grab those first. [Use this guide to update](https://support.apple.com/en-us/HT201541).

### You and your terminal

Your terminal is going to be your BFF, so it might as well not look terrible.

Open `Terminal`. It can be found in your `Applications` folder, or, search for it with `Spotlight` – it's the cute little magnifying glass at the top right of your screen next to your name. Type `Terminal` and it should come right up!

Currently it's just a white box with some scary, unreadable black text. Let's fix that.

With `Terminal` in focus, open the `Preferences`. Up at the top of the box, click on `Profiles` and pick a cute color scheme that speaks to you from the side menu, or get crazy and click that little `+` at the bottom of the menu and make your own. At the bottom of the side menu next to the `+` you'll see a button for   `Default` – click that after you've made your selection.

![terminal preferences window](http://i.imgur.com/Oaphc7L.png)

Beautiful! There's a whole world of color schemes out there that go beyond the defaults (and this article). We encourage you to seek them out when you want to spice things up!

### Xcode Command Line Tools

In your terminal, run this command:

```sh
xcode-select --install
```

Your computer should send you some kind of prompt to install the tools. This'll take a minute...

If it doesn't prompt you, or you get some kind of error, you'll have to [get them from Apple](https://developer.apple.com/downloads/index.action).

Search for "command line tools" in the top left and download the one that matches your version of OSX.

### Show invisible files

Run this command in your terminal to show hidden files in Finder:

```sh
defaults write com.apple.finder AppleShowAllFiles YES
```

Next, you'll need to restart Finder for the change to take effect.

```sh
killall Finder
```

In the next Finder window you open, you'll start seeing hidden files!