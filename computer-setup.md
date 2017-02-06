# Set up your News Apps environment

Welcome to the News Apps team! We know you're probably dying to get started, but first there are a few things we have to do to get it ready for all the cool stuff you're going to build.

- [Pre-setup](#pre-setup)
  - [Make sure you're the admin](#make-sure-youre-the-admin)
  - [Check for OSX updates](#check-for-osx-updates)
  - [You and your terminal](#you-and-your-terminal)
  - [Xcode Command Line Tools](#xcode-command-line-tools)
- [Code editors](#code-editors)
  - [Sublime Text 3](#sublime-text-3)
    - [Wait, why version 3 instead of version 2?](#wait-why-version-3-instead-of-version-2)
    - [Hook Sublime Text 3 into your terminal](#hook-sublime-text-3-into-your-terminal)
  - [Atom](#atom)
    - [Hook Atom into your terminal](#hook-atom-into-your-terminal)
    - [Suggested reading](#suggested-reading)
- [Installing Homebrew](#installing-homebrew)
  - [Installation](#installation)
  - [You and your `.bash_profile`](#you-and-your-bash_profile)
- [Installing Python](#installing-python)
  - [Virtual environments](#virtual-environments)
    - [Installing `virtualenv` and `virtualenvwrapper`](#installing-virtualenv-and-virtualenvwrapper)
    - [Creating a virtual environment](#creating-a-virtual-environment)
- [Installing Node.js](#installing-nodejs)
  - [Installing Gulp](#installing-gulp)
    - [What's npm?](#whats-npm)
    - [What does -g mean?](#what-does--g-mean)
  - [Installing Grunt](#installing-grunt)
- [Installing Ruby](#installing-ruby)
  - [Sass](#sass)
- [Installing git](#installing-git)
- [Installing Docker](#installing-docker)
  - [Installing VirtualBox](#installing-virtualbox)
  - [Installing boot2docker](#installing-boot2docker)
- [Installing PostgreSQL](#installing-postgresql)
- [awscli and SSH](#awscli-and-ssh)

Want to go the extra mile? Check these out.

[&#9733; Bonus Rounds! &#9733;](#-bonus-rounds-)
- [Show invisible files](#show-invisible-files)
- [Hub](#hub)


## Pre-setup

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

## Code Editors

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

## Installing Homebrew

Homebrew describes itself as "The missing package manager for OSX." This means that it helps with the installation of many of the tools you'll use. It also gives you little beers for every package you install, so that's fun.

### Installation

[Go to Homebrew's site](http://brew.sh/), look for `Install Homebrew`, and grab the command there. Because it could potentially change, we won't be providing that command here, but it should start with something that looks like `ruby -e "$(curl...`.

It'll then ask for your computer's admin password – normally this isn't a good idea, but this will prevent you from ever having to run a command with `sudo`.

Next, run Homebrew's status check:

```sh
brew doctor
```

This will make sure everything is cool. If you get any warnings, we'll need to handle those before moving forward. Do what it asks – or grab someone else on the team for help – until `brew doctor` comes back clean.

Now we need to tell our computer where our cool new package manager and all of the packages live.

### You and your `.bash_profile`

Your `.bash_profile` is a hidden file that live in your root directory. Your `.bash_profile` is where settings for your terminal belong.

The easiest way to edit your `.bash_profile` with your text editor we installed earlier. In a freshly opened terminal window, run either `subl .bash_profile` or `atom .bash_profile`. (You can always do it with vim – `vim .bash_profile` – too.)

Add this to the top of your `.bash_profile`:

```sh
export PATH=/usr/local/bin:$PATH
```

This tells your terminal to look in `/usr/local/bin` folder for commands you run before hunting for it somewhere else in your `$PATH`. It just so happens that `/usr/local/bin` is where Homebrew installs commands, so this will ensure you are using the Homebrew packages we install. Save this file.

Now you'll need to either open a new terminal window – which will make the `.bash_profile` file load – or `source` it directly. Don't forget to do this every time you make a change!

```sh
source .bash_profile
```

## Installing Python

The first Homebrew package we're going to install is Python. "But wait," you say, "my computer already has Python!"

You're right! But it's a good idea to not monkey around with your computer's installed software. There's some fragile stuff in there that your computer depends on to function, so we try our best not to disturb it. Plus it is much easier to troubleshoot if you know exactly where your version of Python lives.

Homebrew has [dedicated an entire document](https://github.com/Homebrew/homebrew/blob/master/share/doc/homebrew/Homebrew-and-Python.md) to how it works with Python. It's worth a quick read.

The Data Visuals team defaults to **Python 3**. So we'll install both Python 2 and 3.

```sh
brew install python
pip install --upgrade setuptools pip
pip install --upgrade

brew install python3
pip3 install --upgrade setuptools pip wheel
```

### Virtual environments

When you start working on group projects, it's important to make sure that everyone's working environment is as close to identical as possible. Virtual environments keep a Python project's installs in their own little boxes so there are no conflicts between versions being used in other projects, or those already installed on your computer.

#### Installing `virtualenv` and `virtualenvwrapper`

Run this command in your terminal:

```sh
pip3 install virtualenvwrapper
```

To look at a list of what's currently installed in your environment, you can run the following:

```sh
pip3 freeze
```

Now we need to use our `.bash_profile` to set some settings for `virtualenv`.
Open your `.bash_profile` and add these lines:

```sh
export WORKON_HOME=$HOME/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh
```

Save, then `source` your `.bash_profile`.

#### Creating a virtual environment

Virtual environments are created with the `mkvirtualenv` command.

Try it out!

```sh
mkvirtualenv test
```

You'll get some feedback as it installs `pip`, then your new terminal prompt should begin with `(test)`.

To turn off your environment, run `deactivate`.

Great job! You did it!

> HEADS UP! Make sure you **are not in a virtual environment** when installing packages with Homebrew. Things could get weird. Always `deactivate` before any `brew install` commands.

## Installing Node.js

[Node.js](https://nodejs.org/) makes is possible to build server-side apps using JavaScript. At the Tribune, we use it to run our project building tools.

Let's install it! We use [`nvm`](https://github.com/creationix/nvm) to manage versions. Here's a [direct link to the install instructions](https://github.com/creationix/nvm#install-script).

## Installing git

> You'll need a [GitHub](http://github.com/) account and be a member of the Texas Tribune organization. Someone should help you get this set up – don't worry!

To get this started, install git:

```sh
brew install git
```

Now we need to set some defaults for the git client. First we need to your name for commits.

> This should not be your GitHub user account name. It's meant to be your real name – like Jenny Smith – but you are not required to do so. This name will be public and attached to every one of your commits. Feel free to use a pseudonym!

To set your name, run the following:

```sh
git config --global user.name "<your-name>"
```

Next we'll set your email. This needs to be an email account associated with your Github account. Like the name, this email will be publically available and attached to each of your commits. If you don't know which emails are under your GitHub account, you can [check on GitHub](https://github.com/settings/emails).

```sh
git config --global user.email "<your-email>"
```

> Don't want your email public? GitHub can help with that. On the email settings page, there is a setting at the bottom labeled `Keep my email address private`. You can then use the proxy email GitHub provides.

Next we'll set up authentication. The Homebrew install of git adds a helper that allows it to use OSX's built-in Keychain.

Run the following to tell git to use it:

```sh
git config --global credential.helper osxkeychain
```

We also need to tell git to use `https` for cloning.

```sh
git config --global hub.protocol https
```

## Installing Docker

Docker is a tool for containerizing apps. We use it for deploys and database management. You'll need [Docker for Mac](https://docs.docker.com/docker-for-mac/).

## Installing PostgreSQL

Nearly all of our projects use [PostgreSQL](http://www.postgresql.org/) as their backend. Instead of installing it with Homebrew, we use [Postgres.app](http://postgresapp.com/) instead.

Visit [http://postgresapp.com/](http://postgresapp.com/) and download the installer. After installing, run the app. You should get a pop up window and see a cute little elephant romping around in your menu bar in the top right. If you see the elephant, Postgres.app is live.

Next we need to add Postgres.app's folder to our `$PATH` so our terminal can find the PostgreSQL commands. We will do this in our `.bash_profile`.

> Note: This line needs to come **before** what we added for Homebrew. Otherwise, Homebrew's `brew doctor` will throw a fit. This is to ensure that command added by Homebrew are seen before the PostgreSQL commands.

Add this line to the top, then `source .bash_profile`:

`export PATH=/Applications/Postgres.app/Contents/Versions/latest/bin:$PATH`

Run `which psql` in your terminal to make sure your computer recognizes your changes.

## awscli and SSH

For now, it's best to have one us set you up with these. We'll have to send you files that aren't safe to share publicly on the guide.

# &#9733; Bonus Rounds! &#9733;

Below are some things you can set up that aren't necessary, but can be very useful.

## Show invisible files

Run this command in your terminal to show hidden files in Finder:

```sh
defaults write com.apple.finder AppleShowAllFiles YES
```

Next, you'll need to restart Finder for the change to take effect.

```sh
killall Finder
```

In the next Finder window you open, you'll start seeing hidden files!

## Hub

`hub` is an extension for git that adds extra functionality. [Read more about the perks](https://hub.github.com/).

To install, we'll use Homebrew:

```sh
brew install hub
```

Next, we'll need to alias `hub` to point to git in your `.bash_profile`. (Don't forget to `source`!)

```sh
alias git=hub
```
