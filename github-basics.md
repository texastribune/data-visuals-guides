#Github Basics

Congratulations! You made it this far. Welcome to Github- a collaborative space for people to push their code for other people to check it out, pull it down and make changes, and keep track of their changes.

**DISCLAIMER**: this is in no way a comprehensive guide to Github. This is meant to introduce some basic concepts with some step-by-step instructions to document our workflow here at The Texas Tribune. 

##Git & Github: The watered down version

**Git**- Git is not the same as Github. Git is the software aspect of Github. It is a version control system that is accessed through the command line, or Terminal, and it keeps track of changes you make on projects as you work on them. [This is a far more detailed guide](https://git-scm.com/about) then you'll need for now, but it'll be helpful if you ever get stuck.

**Github**- Github is the place where all of your code trcked by Git is hosted so the rest of the world can see it. In addition to all of the cool things Git does, Github also offers lots of great collaboration tools such as wikis, task management, and feature requests. Wikipedia has a pretty good explanation of Github that you can check out [here](http://en.wikipedia.org/wiki/GitHub). 

##Let's get started!

Follow our guide to setting up your News Apps computer to install git.

##Clone

To get a repository (a project folder) from Github and onto your computer, copy the HTTPS clone URL on the right-hand column of the repository, or repo, you're looking for. 

![clone repository](http://i.imgur.com/ZnwYssk.png?1)

Open Terminal on your computer. `cd` to the folder you want this folder to live in (`cd path/to/folder`), and execute the following command: 

`git clone your-copied-url`

Type `ls` into the terminal, and you should see your brand new repo in there! `cd` into that folder (`cd name-of-new-folder`) and get to work.

###Note:
Rarely will you ever have to create your own repository or project, but if you do, this [guide to creating a Git repository](http://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository) is a great place to get started. There are also some more in-depth explanations to some of the things outlined in here that might be worth the browse.

##Commit & Push changes!

So you've made some changes in the code and you're ready to document your work. Commits are basically comments you make on changes. You'll want to do this every time you add or change something in the code. For instance, say you pull down this file and want to add another couple steps- those couple steps you added could be one commit. If you have multiple step-by-step instructions you want to add, each of those should be their own commit. This process is unique to everyone, and it's totally not a big deal if you screw up a commit, but it's a good idea to commit often so you have a solid record of your process for later.

* **Step 1:** you'll first want to check what you've changed. To do this, you'll type the command `git status` into your terminal. It should return a list of all the files that have changed since the last commit. 
* **Step 2:** If these look right to you, then type `git add file/that/has/changed` for each file changed. Alternatively, you could also just `git add .` to add all of the changed files at once. 
* **Step 3:** Now that you've added your files to git locally, you can commit the changes you've made with `git commit -m "a quick sentence about the changes you made"`. Make your commit messages specific and concise. A sentence will do.
* **Step 4:** After you've committed a few changes, you're ready to share your new code with the world and push it up to Github. To do that, you'll `git push origin branch-you're-on` (if you haven't consciously switched branches- you're probably on master. To check you can `git branch` and it'll tell you). Check for errors in the terminal and always double-check on Github to make sure your changes actually got pushed through accurately, and then you're good to go!


##Pulls and Merge Conflicts Aren't so Scary

We did it! We pushed a change and the whole world can see it! But what if someone else pushed their change before yours, and github refuses your change and spits back an error you'll see in your terminal? That's cool- before you start name calling and getting mad, we can just pull their changes down and then push ours up. Here's how:

###Pull

After you `git status`, `git add .`, and `git commit` your changes, try a `git pull` to collect everything pushed up to github that you don't yet have locally. If your terminal returns with no errors, you can continue with a `git commit` (no -m needed here, git knows we're just merging some pulls into your stuff). 

Your terminal will then give you a vim editor page- it's scary looking, but not so bad. It just says that you're merging a pull. All you need to do is type `ZZ` to get out of there. Then do a `git push` and get back to what you were doing.

###OH NO! I GOT A CONFLICT!

Unless you and your teammates are working on the same folder at the same time, you shouldn't have to worry about the dreaded `CONFLICT` that could appear in your terminal. But if you did get a `CONFLICT`, it's okay! You're going to be fine! I'm going to walk you through it.

* **Step 1:** Read the conflict error in your terminal. It should tell you the exact file(s) where the conflict exists. Go to those files in your text-editor of choice and see what's up.
* **Step 2:** If you scoll through those files, you should see a bunch of `>>>>>>>>` and `<<<<<<<<` with some other stuff in your code. If you and your teammate edited the same thing and did something different- double-check that you're not deleting something they need. Otherwise, keep what you need and delete those weird characters. That's right- it's as easy as deleting what you don't want.
* **Step 3:** Run `git status` to make sure you got everything. Make sure all of the files that had a `CONFLICT` are now showing up in the list of edited files so you know you got everything. Then `git add .` to add all of your changes.
* **Step 4:** `git commit` - Again- git knows you're only merging conflicts- you don't really need a message here, but it will bring you back to the vim text editor (another `ZZ` will get you back to where you need to be).
* **Step 5:** Push up your merge. `git push origin branch-you're-on` You did it! Crisis averted.

##Branches, Merges and Pull Requests

Let's say one of your teammate's is working on a project, but there are a few items on the Basecamp to-do list that are assigned to you. Some of those items might conflict with what they're working on, and you don't want to get in their way. No problem! Once you're in the project in your terminal, let's make a branch. 

Branches are basically like making a copy of the big project as it is when you branch off, and working on the copy rather than the big project. What you do on the branch will not affect the whole project until you merge it in. 

Branches are meant to be disposable, and only do one or two things (such as restyle a form, or add a feature) _not to redo an entire section of a website_. Branches are primarily for features or changes you don't want to add to the big project until they're completely done and checked over by another teammate.

Don't be afraid to make tons of branches and delete them as you merge them back into the big project. Branches are your friend. They keep everyone organized, they're another way to document the process, and they prevent you from royally screwing everything up when you brilliant feature actually turns out to be not so brilliant. (This is confusing and scary at first, [this handy workflow model](http://nvie.com/posts/a-successful-git-branching-model/) might help make it a little clearer.)


###To make a branch:

`git checkout -b name-of-branch` in your terminal. Great job! You made a branch. To make sure it worked, you can `git branch` to return a list of branches. If you want to go to another branch that already exists, you can 'git checkout name-of-branch-you-want-to-work-on' and it'll send you there.

As you're working in your branch, you'll do all of your `git status`, `git add` and `git commit`'s the same, but you'll have to `git push origin name-of-branch` so git knows where to put your changes. If you need to pull something from your branch, you'll also have to do a `git pull origin name-of-branch`.

###Merge master into your branch:

When you're done with all of your your changes and ready to add this branch to the master branch, it's always a good idea to **merge** the master branch _into_ your branch. This saves your teammate form having to fight too hard with your branch when they try to merge it into their project.

* **Step 1:** `git checkout master` This gets you out of your branch and back on the main branch.
* **Step 2:** `git pull origin master` This collects all of the changes on master that may have happened while you were working on your branch (remember that your branch is only as recent as when you made it) syncs it with your master branch
* **Step 3:** `git checkout name-of-your-branch` This sends you back to your branch
* **Step 4:** `git merge master` This brings over all of the changes that have happened on master since you started your branch. You might see a conflict, but that's okay- we already talked about those and know they're not so bad. Go ahead and fix them.
* **Step 5:** When everything's clear and you don't have any more errors, you can `git commit` followed by a `git push origin name-of-your-branch` all done!


###Your first pull request!!

So you're done with your changes and you're ready to see if your teammate wants to pull your changes into the big project. Cool! That's what a **pull request** is for.

* **Step 1:** Go to the project on Github. On the right-hand side, you should see a little icon that looks like this:
![pull request icon](http://i.imgur.com/xBlJKPF.png?1)
* **Step 2:** Click it, and click the ![new pull request](http://i.imgur.com/itaLpTX.png?1) button.
* **Step 3:** At the top, you'll see two dropdown menus. One says 'base', the other says 'compare'. 9 times out of 10, the 'base' is going to be the master branch. 100% of the time, your-branch-name is going to be 'compare'.
![base and compare](http://i.imgur.com/4gtwcLx.png?1)
* **Step 4:** Fill in the text boxes! The title of the pull request can be the name of the branch, or it can be the name of the to-do on basecamp. Make your description specific. If you changed something visual (made a button look different, added a template, whatever) plz include a screenshot shot in your description.
* **Step 5:** After you've submitted your pull request, send a link to the rest of the team so someone can look over it and merge it in. 

If you're ever asked to merge in a pull request- just click the merge button.
![This pull request can be automatically merged](http://i.imgur.com/25nVRSY.png)
It should say 'This pull request can be automatically merged' because the owner of the pull request should have merged master before requesting the pull. Otherwise, the button will be purple and you might have to resolve some conflicts.

##You did it!

Nice work. Now you know pretty much everything you need to know about Github for what we'll be using it for here. There are tons of resources and helpful tools you can use to make Github and Git everything you want it to be and more. To get you started, here are a few of our favorites:


* [Make some aliases](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases) to make your already very short git commands even shorter
* [Hub](https://hub.github.com/)- we go over how to set this as a bonus round when setting up your News Apps computer. It makes some commands like switching between branches and commits slightly less cryptic.
* Autocomplete- I don't have a link for this, help a sister out.


