#Set up your News Apps Environment

Welcome to the Tribune! Your new computer is super shiny and I know you're probably dying to get started, but first- there are a few things we have to do to get it ready for all the cool stuff you're going to build.

This guide is based loosely on [this guide](http://blog.apps.npr.org/2013/06/06/how-to-setup-a-developers-environment.html) by our friends at NPR Visuals.

##The Basics

###Make sure you're the admin
Go to system preferences
Click on Users & groups
Do you see your name with Admin written below it on the left? Awesome! You're the admin.
Otherwise, go bug IT (or in our case, Rodney) and ask to be the admin.

![are you the admin?](http://i.imgur.com/rTsdp5C.png?1)

###Check for updates
Go to the App Store
Make sure you don't have any updates hanging out up there
Update them and reboot as necessary

###You and your terminal
Your terminal is going to be your bff for a little while, so you might as well make it not look so terrible. Here's how to make it not look quite so blinding and gross.

Open terminal. You can either find it in your Applications folder, or find it with Spotlight (that cute little magnifying glass at the top right of your screen next to your name). Type 'terminal' and it should come right up.

You'll notice that it's just a white box with some scary, unreadable black text. Let's fix that.

Under terminal up at the top, click on Preferences. Up at the top of the preferences box, click on 'Profiles' and pick a cute color scheme that speaks to you from the side menu, or get crazy and click that little + at the bottom of the menu and make your own. At the bottom of the side menu next to the +, you'll see a button for Default- click that when you've made your selection.

![terminal preferences window](http://i.imgur.com/Oaphc7L.png)

Beautiful!

###Show invisible files
Run this command `defaults write com.apple.finder AppleShowAllFiles YES` in terminal, and relaunch Finder.

This'll make it easier to find things like .git folers or your .bash_profile and to open files and folders stright from your terminal.

###Install Sublime
Click [here](http://www.sublimetext.com/3)
Install the IOS one

Run this command in your terminal:
`ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl`
Now, everytime you type `subl /path/to/folder` in your terminal, it will open whatever file or folder you tell it to in Sublime and you will be super happy.

We'll worry about setting up the other cool stuff on Sublime later, it's just handy to have now for some of the stuff we'll do for set up later.

###X-Code Command Line Tools
NOT THE X-CODE APP unless you want to die waiting for it to install on your computer and deal with daily annoying and terrible updates.

Instead run this command:
`xcode-select --install`

Your computer should send you some kind of prompt to install the tools- do that.

This'll take a minute...

If it doesn't prompt you, or you get some kind of error, you'll have to get them from Apple [developer.apple.com/downloads/index.action](developer.apple.com/downloads/index.action). 

Search for "command line tools" on the top left and download the one that matches your version of OS X. Yay!

##Homebrew

Homebrew describes itself as 'The missing package manager for OSX'. Basically that means that it installs a bunch of tools you'll use all the time (python, Node, etc.) in one simple step and it stores them all in the same place. It also gives you little beers for every package you install, so that's fun. For more fun stuff about Homebrew and Python and the other fun stuff it does, you [check this out](http://docs.python-guide.org/en/latest/starting/install/osx/).

Click [here](http://brew.sh/) to go to brew.sh

Scroll down to Install Homebrew, and copy that line of code underneath it. It should look something like:

`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Or you could just type that- but just in case they change it on us, we want to make sure you can find it.

It'll then ask for your computer password, so type that. Then do a `brew doctor` to make sure everything's cool. We like to be super thorough around here, so open a new tab in your terminal and type `brew doctor` again. Still cool? Righteous. Moving on.

Before we start installing things willy nilly, we should probably make sure we grabbed the most recent version of brew, `brew update`

Now we need to tell our computer where our cool new package manager and all of its packages lives.

###You and your `.bash_profile`

Your `.bash_profile` is one of those invisible files that live in your root (the root is the base level of where files on your computer live. Things like the Applications folder and Desktop live here). Your `.bash_profile` is what keeps all of your custom envirnment variables for your terminal, or command line, set.

The easiest way to edit your `.bash_profile` is to `subl ~/.bash_profile`. You can always do it with vim (`vim ~/.bash_profile`) or nano (`nano ~/.bash_profile) or your text editor of choice.

We'll be doing a lot of monkeying around in our `.bash_profile`, so best to get comfortable with it now.

Copy and paste this into your `.bash_profile`:

`export PATH=/usr/local/bin:$PATH`

This tells your computer that you're handing Homebrew the reins to update and maintain its packages. Save it. Now you'll need to source it. 

Any time you edit your `.bash_profile` you'll need to let your computer know aboutt he changes. Do this by running `source .bash_profile` in your terminal.

####WARNING about Homebrew

Don't get weird and start brew installing when you're in a virtual environment (we'll get to those later). You're going to have a bad time.

##Python

The first Homebrew package we're going to install is Python. 

You say: "But Mac already has Python!" 

I know- but it's usually a good idea to not monkey around too much in your computer's installed software. There's some fragile stuff in there, plus it's much easier to troubleshoot if you know exactly where your Python came from and lives.

Find the docs for Homebrew Python [here](https://github.com/Homebrew/homebrew/blob/master/share/doc/homebrew/Homebrew-and-Python.md)

* **Step 1:** `brew install python` 
* **Step 2:** `pip install --upgrade setuptools`
* **Step 3:** `pip install --upgrade pip` 

##Virtual Environments

Virtual environments aren't as scary as they sound. When you start working on group projects, chances are everyone's computer is set up differently. Maybe they have a different version of something, or maybe they don't already have something installed. 

Virtualenv keeps all of your python projects in their own little boxes so everyone's installs are on the same page.

Learn more about virtual environments [here](https://virtualenvwrapper.readthedocs.org/en/latest/)

###To install:

`pip install virtualenvwrapper` in your terminal

Check it with `pip freeze` and you should see it listed there.

Open your .bash_profile (run `subl ~/.bash_profile` in your terminal)

and copy and paste these into your text editor:

`export WORKON_HOME=$HOME/.virtualenvs`

and

`source /usr/local/bin/virtualenvwrapper.sh`

Save it in your text editor, and source it (`source .bash_profile`) in your terminal

Run this: `mkvirtualenv test` in your terminal to test it

Did it work? Yay!

`deactivate` in your terminal turns it off.

Great job! You did it!

##Node

Node is another package manager. You can never have too many package managers.

Run `brew install node` in your terminal to install it...

`which node` should tell you it's in your bin/local

###Gulp

Now that we have Node, we can install all the things that use it like Gulp. Basically- Gulp is what pushes your changes to your local server as you save things in your text editor so you don't have to refresh every time.

`npm install -g gulp` in your terminal installs it

(`-g` means global- so you don't have to install it again for every project)

`which gulp` should tell you where it is, which should be `local/bin/gulp`

###Grunt

Grunt is basically the same as Gulp, we just don't use it anymore for newer projects. Mainly we're installing this in case we need to update an older project that uses Gulp.

Run `npm install -g grunt -cli`

Yay done with Node!

##Ruby

It's going to be okay. We only use Ruby for our Sass- the language we use to write our CSS that makes our graphics beautiful.

`brew info rbenv` in your terminal.

There should be an if statement in there that looks something like:

`if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi`

Copy that.

Then run `brew install rbenv`

Followed by `brew install ruby-build`

(Keep that if statement you copied earlier. We'll need it shortly.)

`brew info ruby-buld`

Then put that if statement you copied in your .bash_profile (`subl ~/.bash_profile`)

Source it (`source .bash_profile`)

Run `which rbenv` ...Is it in there? Yay!

Run `rbenv install -l` and scroll down to see which version is the newest, the one just before the version number -dev (as of today it's 2.2.2)

Then install it with `rbenv global 2.2.2` or whatever version number you have.

###Sass

Sass is our CSS extension language of choice. 

Learn more about it [here](http://sass-lang.com/) 

Run `gem install sass` followed by `which sass` to make sure it's in there.

##Git

This assumes you already have a github.com login with The Texas Tribune and have access to our repositories. It's a pretty inrense 

First run `brew install git`

Then `git config --global user.name "yourname"` Your user name can really be whatever you want your commits to be listed as. 

Then set up your email/github account with one of the email accounts associated with your github account 

`git config --global user.email "email@email.com"` 

If you don't know which emails are under your github account, you can check by going to github.com, clicking the gear in the top right, and finding 'emails' in the side menu. 

Anyway... back to terminal. Run `git credential -osxkeychain`

Then `git config --global credential.helper osxkeychain`

Make a folder to put all of your news apps in somewhere on your computer. I have mine on my Desktop, some people put theirs at the root, but you can put it anywhere.

`cd` to your folder, (for me it's `cd Desktop/trib`) and clone a project in there to test it (if you're new to github, you can learn how to clone [here]()) 

Oh no! It wants a ~*token*~! What's that??

###Personal Access Tokens

Personal access tokens authenticate with github (like when you're pulling/pushing to a private repo) so it can check against this rather than you typing in your password every time.

Get one of these puppies by going back up to your gear in the top right, finding Persona access tokens in the side menu, and clicking the generate a new token button.

It'll ask for a name- most of us call it terminal- but it can be whatever you want your new special snowflake token to be called. Beneath the Token description, you'll see 'Select scopes' with a bunch of check-boxes. Check 'repo', 'gist', and 'user'.

Finally, click the 'Generate token'

Copy and paste the string of whatever it spits out into your terminal... Did it work?

Quit terminal, reopen, and try to clone something else into your folder. You might have to do the `cd where/your/folder/lives` to get back to where your github repositories live.

Yay! Congratulations on your new special snowflake token.

###Two Factor Auth

For security!

Download some kind of auth app on your smartphone. There are, like, a million, and most of them are free. I use Google Authenticator and it seems to work great, some of us use Duo Mobile- whatever, just get one.

Open the app and follow the instructions...

It'll eventually ask you to go to github.com and scan a code or do something with a code. Click the gear in the top right, find 'Security' in the side menu, go to Set Up 2 Factor Auth' and follow the instructions.

Once it's finished, it'll ask you if you want to save the alternate auth files- *YOU DO*. This is in case you don't have your phone anymore, something weird happened, or you're stranded on an island- you might need these. Print them out, save them in your drafts, put them in some weird file, put them in your Dropbox, whatever you do- just keep them.


####BONUS ROUND: HUB

*You don't need this. It's just a cool thing we use sometimes.*

Hub is a fun git extension that adds some extra commands like git browse that will open your browser to whatever folder you're in on github.com. Read more about it [here](https://hub.github.com/)

`brew install hub`

`which hub` ...should be in there

Next you'll need to alias hub to point to git in your .bash_profile

Paste `alias git=hub` in your .bash_profile

Then `source .bash_profile`

And finally, `git config --global hub.protocol https` so it knows where to look when you're cloning things.

##DOCKER

Docker is a virtual environment we use to keep and manage databases. The idea is that it's intened to emulate a shipping dock, hence 'Docker' with a bunch of containers that hold things and have their own little environments inside.

This one's complicated, so let's take it step-by-step.

* **Step 1:**First thing, go to the Internet and download [Virtual Box](https://www.virtualbox.org/wiki/Downloads)
* **Step 2:** Quit your terminal.
* **Step 3:** Open it back up, and `brew install boot2docker`
* **Step 4:** `boot2docker init`
* **Step 5:** `boot2docker up`
* **Step 6:** After you start it up, it'll tell you some stuff to put in your .bash_profile (everything with export in front of it). Copy those and put those in your .bash_profile (`subl ~/.bash_profile`)
* **Step 7:** Source it. `source .bash_profile`
* **Step 8:** `docker version` should give you a bunch of stuff about what you just did...

And you did it! You now have Docker installed. Great job!

##Postgres

Go to [postgresapp.com](http://postgresapp.com/) and download the app.

Open it up (might have to spotlight it) and you should see a cute little elephant up in your very top browser next to your battery and wifi stuff on your computer. Look for that if you ever want to know if it's running.

Go back to [postgresapp.com](http://postgresapp.com/) and scroll down to where it says 'Quick Installation Guide'. Copy and paste the stuff on step 3 at the very top of the `.bash_profile`. It should look something like this:

`export PATH=/Applications/Postgres.app/Contents/Versions/9.4/bin:$PATH`

Then, of course, `source .bash_profile`

Back to your terminal, run `which psql` to make sure your computer recognizes it, and `brew doctor` to make sure everyone's happy.

##AWS & SSH

Bug us about getting you set up with these. We have special news apps ones.





