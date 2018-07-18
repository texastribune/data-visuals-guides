# Set up your News Apps environment

Welcome to the News Apps team! We know you're probably dying to get started, but first there are a few things we have to do to get it ready for all the cool stuff you're going to build.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
- [Set up your News Apps environment](#set-up-your-news-apps-environment)

  - [Pre-setup](#pre-setup)
    - [Make sure you're the admin](#make-sure-youre-the-admin)
    - [Check for MacOS updates](#check-for-macos-updates)
    - [You and your terminal](#you-and-your-terminal)
  - [Code Editors](#code-editors)
    - [Atom](#atom)
      - [Hook Atom into your terminal](#hook-atom-into-your-terminal)
      - [Suggested reading](#suggested-reading)
    - [Sublime Text](#sublime-text)
      - [Hook Sublime Text into your terminal](#hook-sublime-text-into-your-terminal)
  - [Installing Homebrew](#installing-homebrew)
    - [Installation](#installation)
  - [Installing Python](#installing-python)
    - [Virtual environments](#virtual-environments)
      - [Installing `virtualenv` and `virtualenvwrapper`](#installing-virtualenv-and-virtualenvwrapper)
      - [Creating a virtual environment](#creating-a-virtual-environment)
  - [Installing Node.js](#installing-nodejs)
  - [Installing git](#installing-git)
  - [Installing Docker](#installing-docker)
  - [Installing PostgreSQL](#installing-postgresql)
  - [awscli and SSH](#awscli-and-ssh)
- [&#9733; Bonus Rounds! &#9733;](#9733-bonus-rounds-9733)
  - [Show invisible files](#show-invisible-files)
  - [Hub](#hub)
  - [But I need Python 2!](#but-i-need-python-2)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Pre-setup

### Make sure you're the admin

Everything we do here is only going to work if you have admin privileges. How do you know if you have it?

1. Open your `System Preferences`.
2. Click on `Users & Groups`.
3. Do you see your name with `Admin` written below it on the left? Awesome! You're the admin.

![Are you the admin?](http://i.imgur.com/rTsdp5C.png?1)

Don't have admin powers? Reach out to [Rodney](rgibbs@texastribune.org) and he'll get you set up.

### Check for MacOS updates

If your computer is brand new, you may have a few outstanding operating system updates. Make sure to grab those first. [Use this guide to update](https://support.apple.com/en-us/HT201541).

### You and your terminal

The terminal is going to be your BFF, so it might as well not look terrible.

Open `Terminal`. It can be found in your `Applications` folder, or, search for it with `Spotlight` – it's the cute little magnifying glass at the top right of your screen next to your name. Type `Terminal` and it should come right up!

Currently it's just a white box with black text. Let's fix that.

With `Terminal` in focus, open the `Preferences`. Up at the top of the box, click on `Profiles` and pick a cute color scheme that speaks to you from the side menu, or get crazy and click that little `+` at the bottom of the menu and make your own. At the bottom of the side menu next to the `+` you'll see a button for   `Default` – click that after you've made your selection.

![terminal preferences window](http://i.imgur.com/Oaphc7L.png)

Beautiful! There's a whole world of color schemes out there that go beyond the defaults (and this article). We encourage you to seek them out when you want to spice things up!

## Code Editors

Two editors are used here at The Texas Tribune – [Atom](https://atom.io/) and [Sublime Text](http://www.sublimetext.com/). We have no particular preference – try them both out! (You're welcome to use anything else, too.)

### Atom

[Download the installer](https://atom.io/) and install as normal.

#### Hook Atom into your terminal

Atom does this automatically on install. You should be able to type `atom <path>` in your terminal to open files and folders with Atom.

#### Suggested reading

Check out the [Atom Flight Manual](http://flight-manual.atom.io/) – it's a good overview on how Atom works.

### Sublime Text

[Download the installer](http://www.sublimetext.com/) and install as normal.

#### Hook Sublime Text into your terminal

If you want to be able to open Sublime Text from your Terminal, you'll need to [follow this guide](https://www.sublimetext.com/docs/3/osx_command_line.html).

Now you can type `subl <path>` in your terminal and Sublime will open that file or folder.

## Installing Homebrew

Homebrew describes itself as "The missing package manager for MacOS." This means that it helps with the installation of many of the tools you'll use.

### Installation

First, we need to make sure your OS and Xcode is cool with Homebrew. Run this in your terminal:

```sh
xcode-select --install
```

[Go to Homebrew's site](http://brew.sh/), look for `Install Homebrew`, and grab the command there. Because it could potentially change, we won't be providing that command here, but it should start with something that looks like `ruby -e "$(curl...`.

It'll then ask for your computer's admin password – normally this isn't a good idea, but this will prevent you from ever having to run a command with `sudo`.

Next, run Homebrew's status check:

```sh
brew doctor
```

This will make sure everything is cool. If you get any warnings, we'll need to handle those before moving forward. Do what it asks – or grab someone else on the team for help – until `brew doctor` comes back clean.

Now we need to tell our computer where our cool new package manager and all of the packages live.

## Installing Python

The first Homebrew package we're going to install is Python. "But wait," you say, "my computer already has Python!"

You're right! But it's a good idea to not monkey around with your computer's installed software. There's some fragile stuff in there that your computer depends on to function, so we try our best not to disturb it. Plus it is much easier to troubleshoot if you know exactly where your version of Python lives.

Homebrew has [dedicated an entire document](https://github.com/Homebrew/homebrew/blob/master/share/doc/homebrew/Homebrew-and-Python.md) to how it works with Python. It's worth a quick read.

The Data Visuals team defaults to **Python 3**. If are in the rare situation where you still need **Python 2**, let someone know and we can help.

```sh
brew install python
pip install --upgrade setuptools pip wheel
```

### Virtual environments

When you start working on group projects, it's important to make sure that everyone's working environment is as close to identical as possible. Virtual environments keep a Python project's installs in their own little boxes so there are no conflicts between versions being used in other projects, or those already installed on your computer.

#### Installing `virtualenv` and `virtualenvwrapper`

Run this command in your terminal:

```sh
pip install virtualenvwrapper
```

To look at a list of what's currently installed in your environment, you can run the following:

```sh
pip freeze
```

Now we need to use our `.bash_profile` to set some settings for `virtualenv`.
Open `~/.bash_profile` and add these lines:

```sh
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=$(which python3)
source /usr/local/bin/virtualenvwrapper.sh
```

Save, then run `source ~/.bash_profile`.

#### Creating a virtual environment

Virtual environments are created with the `mkvirtualenv` command.

Try it out!

```sh
mkvirtualenv test
```

This will create a Python 3 environment. You'll get some feedback as it installs `pip`, then your new terminal prompt should begin with `(test)`.

To turn off your environment, run `deactivate`.

Great job! You did it! 

To go back to your enivronment, you can run `workon test`. To list all the virtual environments you've created, run `lsvirtualenv`.

> HEADS UP! Make sure you **are not in a virtual environment** when installing packages with Homebrew. Things could get weird. Always `deactivate` before any `brew install` commands.

## Installing Node.js

[Node.js](https://nodejs.org/) makes is possible to build server-side apps using JavaScript. At the Tribune, we use it to run our project building tools.

Let's install it! We use [`nvm`](https://github.com/creationix/nvm) to manage versions. Here's a [direct link to the install instructions](https://github.com/creationix/nvm#install-script).

Now, if you run `nvm ls-remote`, you'll be able to see all the versions of Node.js that are available.

We currently base all of our projects on the current Long-term Support (LTS) version. Currently, that's `Node.js 8`.

To install that, run the following:

```sh
nvm install lts/carbon
```

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

Next we'll set your email. This needs to be an email account associated with your Github account. Like the name, this email will be publicly available and attached to each of your commits. If you don't know which emails are under your GitHub account, you can [check on GitHub](https://github.com/settings/emails).

```sh
git config --global user.email "<your-email>"
```

> Don't want your email public? GitHub can help with that. On the email settings page, there is a setting at the bottom labeled `Keep my email address private`. You can then use the proxy email GitHub provides.

Next we'll set up authentication. The Homebrew install of git adds a helper that allows it to use MacOS's built-in Keychain.

Run the following to tell git to use it:

```sh
git config --global credential.helper osxkeychain
```

We also need to tell git to use `https` for cloning.

```sh
git config --global hub.protocol https
```

For more information on git and GitHub, check out [this interactive tutorial](https://try.github.io/) or [this walk through](https://guides.github.com/activities/hello-world/) to get started.

## Installing Docker

Docker is a tool for containerizing apps. We use it for deploys and database management. You'll need [Docker for Mac](https://docs.docker.com/docker-for-mac/).

## Installing PostgreSQL

Nearly all of our projects use [PostgreSQL](http://www.postgresql.org/) as their backend. Instead of installing it with Homebrew, we use [Postgres.app](http://postgresapp.com/) instead.

Visit [http://postgresapp.com/](http://postgresapp.com/) and download the installer. After installing, run the app. You should get a pop up window and see a cute little elephant romping around in your menu bar in the top right. If you see the elephant, Postgres.app is live.

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
