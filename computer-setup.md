#Set up your News Apps Environment

Welcome to the Tribune! Your new computer is super shiny and ready to get started, but first- there are a few things we have to do to get it ready for all the cool stuff you're going to build.

##The Basics

###Make sure you're the admin
Go to system preferences
Users & groups
Do you see your name with Admin written below it? Awesome! You're the admin.

###Check your apps
Go to the App Store
Make sure you don't have any updates hanging out up there
Update them if you do

###You and your Terminal
Your Terminal is going to be your bff for a little while, so you might as well make it not look so terrible. Here's how to make it not look quite so blinding and gross.

###Show invisible files
Run this command `defaults write com.apple.finder AppleShowAllFiles YES`
And relaunch Finder.

This'll make it easier to find things like .git folers or your .bash-profile

###Install Sublime
Click [here](http://www.sublimetext.com/3)
Install the IOS one

Run this command in your terminal:
`ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl`
Now, everytime you type `subl /path/to/folder` in your terminal, it will open whatever file or folder you tell it to in Sublime and you will be super happy.

We'll worry about setting up the other cool stuff on Sublime later, it's just handy to have now for some of the stuff we'll do for set up.

###X-Code Command Line Tools
NOT THE X-CODE APP unless you want to die waiting for it to install on your computer and deal with daily annoying and terrible updates.

Instead run this command:
`xcode-select --install`

This'll take a minute...

##Homebrew

Homebrew describes itself as 'The missing package manager for OSX'. Basically that means that it installs a bunch of tools you'll use all the time (python, Node, etc.) in one simple step and it stores them all in the same place. It also gives you little beers for every package you install, so that's fun.

Click [here](http://brew.sh/) to go to brew.sh

Scroll down to Install Homebrew, and copy that line of code underneath it. It should look something like:

`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Or you could just type that- but just in case they change it on us, we want to make sure you can find it.

It'll then ask for your computer password, so type that. Then do a `brew doctor` to make sure everything's cool. We like to be super thorough around here, so open a new tab in your terminal and type `brew doctor` again. Still cool? Righteous. Moving on.

Before we start installing things willy nilly, we should probably make sure we grabbed the most recent version of brew, `brew update`

Now we need to tell our computer where our cool new package manager and all of its packages lives.

Open your .bash_profile. This is one of those invisible files that live in your root. The easiest way to edit your bash-profile is to `subl ~/.bash-profile`- but you can always do it with Vim or your text editor of choice.

Copy and paste this into your .bash-profile:

`export PATH=/usr/local/bin:$PATH`

Great job! Now it's time to do fun stuff.

####WARNING

Don't get weird and start brew installing when you're in a virtual environment (we'll get to those later). You're going to have a bad time.

##Python

First package we're going to install is Python. 

You say: "But Mac already has Python!" 

I know- but it's usually a good idea to not monkey around too much in your computer's installed programs. There's some fragile stuff in there, plus it's much easier to troubleshoot if you know exactly where your Python came from and lives.

Find the docs for Homebrew Python [here](https://github.com/Homebrew/homebrew/blob/master/share/doc/homebrew/Homebrew-and-Python.md)

* **Step 1:** `brew install python`
* **Step 2:** `pip install --upgrade setuptools`
* **Step 3:** `pip install --upgrade pip` 

##Virtual Environments

Virtual environments aren't as scary as they sound. When you start working on group projects, chances are everyone's computer is set up differently. Maybe they have a different version of something, or maybe they don't already have something installed. 

Virtual environments put everyone on the same page. Before you start a big project, you'll probably have to make a virtual environment (`mkvirtualenv`) and install a bunch of stuff. This makes sure that everyone has the same packages and prevents weird problems that are only happening on your computer.

Learn more about virtual environments [here](https://virtualenvwrapper.readthedocs.org/en/latest/)

###To install:

`pip install virtualenvwrapper` in your Terminal

Check it with `pip freeze` and you should see it listed there.

Open your .bash-profile (run `subl ~/.bash-profile` in your terminal)

and copy and paste these in there:
`export WORKON_HOME=$HOME/.virtualenvs`
`source /usr/local/bin/virtualenvwrapper.sh`

save it and source it (`source .bash-profile`)

Back to your Terminal, run this: `mkvirtualenv test`

Did it work?

`deactivate` in your Terminal turns it off.

Great job! You did it!

##Node

Node is another package manager. You can never have too many package managers.

Run `brew install node` in your Terminal to install it...

`which node` should tell you it's in your bin/local

###Gulp

Now that we have Node, we can install all the things that use it like Gulp. Basically- Gulp is what pushes your changes to your local server as you save things in your text editor so you don't have to refresh every time.

`npm install -g gulp` in your Terminal installs it

(`-g` means global- so you don't have to install it again for every project)

`which gulp` should tell you where it is, which should be `local/bin/gulp`

###Grunt

Grunt is basically the same as Gulp, we just don't use it anymore for newer projects. Mainly we're installing this in case we need to update an older project that uses Gulp.

Run `npm install -g grunt -cli`

Yay done with Node!

##Ruby

It's going to be okay. We only use Ruby for our Sass stuff.

`brew info rbenv` in your Terminal.

There should be an if statement in there that looks something like:

`if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi`

Copy that.

Then run `brew install rbenv`

Followed by `brew install ruby-build`

(Keep that if statement you copied earlier. We'll need it shortly.)

`brew info ruby-buld`

Then put that if statement you copied in your .bash-profile (`subl ~/.bash-profile`)

Source it (`source .bash-profile`)

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

Anyway... back to Terminal. Run `git credential -osxkeychain`

Then `git config --global credential.helper osxkeychain`

Make a folder to put all of your news apps in somewhere on your computer. I have mine on my Desktop, some people put theirs at the root, but you can put it anywhere.

`cd` to your folder, (for me it's `cd Desktop/trib`) and clone a project in there to test it (if you're new to github, you can learn how to clone [here]()) 

Oh no! It wants a ~*token*~! What's that??

###Personal Access Tokens

Personal access tokens authenticate with github (like when you're pulling/pushing to a private repo) so it can check against this rather than you typing in your password every time.

Get one of these puppies by going back up to your gear in the top right, finding Persona access tokens in the side menu, and clicking the generate a new token button.

It'll ask for a name- most of us call it Terminal- but it can be whatever you want your new special snowflake token to be called. Beneath the Token description, you'll see 'Select scopes' with a bunch of check-boxes. Check 'repo', 'gist', and 'user'.

Finally, click the 'Generate token'

Copy and paste the string of whatever it spits out into your terminal... Did it work?

Quit Terminal, reopen, and try to clone something else into your folder. You might have to do the `cd where/your/folder/lives` to get back to where your github repositories live.

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

Next you'll need to alias hub to point to git in your .bash-profile

Paste `alias git=hub` in your .bash-profile

Then `source .bash-profile`

And finally, `git config --global hub.protocol https` so it knows where to look when you're cloning things.

##DOCKER

Docker is a virtual environment we use to keep and manage databases. The idea is that it's intened to emulate a shipping dock, hence 'Docker' with a bunch of containers that hold things and have their own little environments inside.

This one's complicated, so let's take it step-by-step.

* **Step 1:**First thing, go to the Internet and download [Virtual Box](https://www.virtualbox.org/wiki/Downloads)
* **Step 2:** Quit your terminal.
* **Step 3:** Open it back up, and `brew install boot2docker`
* **Step 4:** `boot2docker init`
* **Step 5:** `boot2docker up`
* **Step 6:** After you start it up, it'll tell you some stuff to put in your .bash-profile (everything with export in front of it). Copy those and put those in your .bash-profile (`subl ~/.bash-profile`)
* **Step 7:** Source it. `source .bash-profile`
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





