# Homebrew

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