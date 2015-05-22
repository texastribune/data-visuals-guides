#Github Basics

Congratulations! You made it this far. Welcome to Github- a collaborative space for people to push their code for other people to check it out, pull it down and add stuff, and keep track of their changes.

##Let's get started!

###Clone###

To get a repository from github and onto your computer, copy the HTTPS clone URL on the right-hand column of the repo you're looking for. Open your terminal, `cd` to the folder you're working in, and execute the following command: `git clone your-copied-url`. Type `ls` into the terminal, and you should see your brand new folder in there! Now you're ready to get cracking.

###Commit & Push changes!###

So you've made some changes in the code and you're ready to commit them to github. This is the intermediary step between pushing your changes onto the github site, and saving them so git knows they're there. You'll want to do this every time you make a change. For instance, say you pull down this file and want to add another couple steps- each step should be its own commit. This process is unique to everyone, but it's a good idea to commit often so you have a solid record of your process for later.

* **Step 1:** you'll first want to check what's changed. To do this, you'll type the command `git status` into your terminal. It should return a list of all the files that have changed since the last commit. 
* **Step 2:** If these look right to you, then type `git add files/that/have/changed`. Alternatively, you could also just `git add .` to add all of the changed files at once. 
* **Step 3:** Now that you've added your files to git locally, you can commit the changes you've made with `git commit -m "a quick sentence about the changes you made"`. Make your commit messages specific, but not an entire paragraph. A sentence will do.
* **Step 4:** After you've committed a few changes (or you need to share what you have with your team) you're ready to share your new code with the world. To do that, you'll `git push origin branch-you're-on`. Always double-check on github to make sure your changes actually got pushed through accurately, and then you're good to go!

###Pulls and Merge Conflicts Aren't so Scary###

We did it! We pushed a change and the whole world can see it! But what if someone else pushed their change before yours, and github refuses your change? That's cool- we'll just pull their changes down and then push ours up. Here's how:

**Pull**- After you've checked the status, added, and committed your changes, try a `git pull` to collect all of the commits pushed up to github that you don't have locally. If your terminal returns with no errors, you can continue with a `git commit` (no -m needed here, git knows we're just merging some pulls into your stuff). 

Your terminal will then give you a vim editor- it's scary looking, but not so bad. It just says that you're merging a pull. All you need to do is type `ZZ` to get out of there. Then do a `git push` and get back to what you were doing.

####OH NO! I GOT A CONFLICT!####

Unless you and your friends are working on the same folder at the same time, you shouldn't have to worry about the dreaded `CONFLICT` that could appear in your terminal. But if you did get a CONFLICT, it's okay! You're going to be fine! I'm going to walk you through it.

* **Step 1:** Read the conflict error in your terminal. It should tell you the exact file(s) where the conflict exists. Go to those files in your text-editor of choice and see what's up.
* **Step 2:** If you scoll through those files, you should see a bunch of >>>>>>>> and <<<<<<<< with some other stuff. If you and your teammate edited the same thing and did something different- double-check that you're not deleting something they need. Otherwise keep what you need and get rid of those weird characters.
* **Step 3:** Do a `git status` to make sure you got everything. Make sure all of the files that had a CONFLICT are now showing up in the list of edited files so you know you got everything. Then `git add` all of your changes.
* **Step 4:** `git commit`! Again- git knows you're only merging conflicts- you don't really need a message here, but it will bring you back to the vim text editor (another `ZZ` will get you back to where you need to be).
* **Step 5:** Push up your merge. `git push origin branch-you're-on` will finish the job and put you back on track.

###Branches, Merges and Pull Requests###

Let's say one of your teammate's is working on a project, but there are a few items on the Basecamp to-do list that are assigned to you. Some of those items might conflict with what they're working on, and you don't want to get in their way. No problem! Once you're in the project in your terminal, let's make a branch. 

`git checkout -b name-of-branch` in your terminal. Great job! You made a branch. To make sure it worked, you can `git branch` to return a list of branches.

As you're working in your branch, you'll do all of your `git status`, `git add` and `git commit`'s the same, but you'll have to `git push origin name-of-branch` so it knows where to put your changes on the Internet. If you need to pull something from your branch, you'll also have to do a `git pull origin name-of-branch`.


When you're done with all of your changes, it's always a good idea to **merge** the master branch into your branch. This saves your teammate form having to fight too hard with your branch.

To do this:

* **Step 1:** `git checkout master` This gets you out of your branch and back on the main branch.
* **Step 2:** `git pull origin master` This gets all of the changes that may have happened while you were working on your branch
* **Step 3:** `git checkout name-of-your-branch` This sends you back on your branch
* **Step 4:** `git merge master` This brings over all of the changes that have happened on master since you started your branch. You might see a conflict, but that's okay- we already talked about those and know they're not so bad.
* **Step 5:**`git commit` & `git push origin name-of-your-branch` all done!

So you're done with your changes and you're ready to see if your teammate wants to pull your changes into the big project. Cool! That's what a **pull request** is for.

* **Step 1:** Go to the project on github.com. On the right-hand side, you should see a little icon that looks like this:
[pull request icon]
* **Step 2:** Click it, and click the 'New Pull Request' button.
* **Step 3:** At the top, you'll see two dropdown menus. One says 'base', the other says 'compare'. 9 times out of 10, the 'base' is going to be master. 100% of the time, your-branch-name is going to be 'compare'.
* **Step 4:** Fill in the text boxes! The title of the pull request can be the name of the branch, or it can be the name of the to-do on basecamp. Make your description specific. If you changed something visual (made a button look different, added a template, whatever) plz include a screenshot shot in your description.



