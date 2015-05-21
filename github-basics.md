#Github Basics

Congratulations! You made it this far. Welcome to Github- a collaborative space for people to push their code for other people to check it out, pull it down and add stuff, and keep track of their changes.

###Let's get started!

**Clone**
To get a repository from github and onto your computer, copy the HTTPS clone URL on the right-hand column of the repo you're looking for. Open your terminal, `cd` to the folder you're working in, and execute the following command: `git clone your-copied-url`. Type `ls` into the terminal, and you should see your brand new folder in there! Now you're ready to get cracking.

**Commit & Push changes!**
So you've made some changes in the code and you're ready to commit them to github. This is the intermediary step between pushing your changes onto the github site, and saving them so git knows they're there. You'll want to do this every time you make a change. For instance, say you pull down this file and want to add another couple steps- each step should be its own commit. This process is unique to everyone, but it's a good idea to commit often so you have a solid record of your process for later.

* **Step 1:** you'll first want to check what's changed- just to be sure. To do this, you'll type the command `git status` into your terminal. It should return a list of all the files that have changed since the last commit. 
* **Step 2:** If these look right to you, then type `git add files/that/have/changed`. Alternatively, you could also just `git add .` to add all of the changed files at once. 
* **Step 3:** Now that you've added your files to git locally, you can commit the changes you've made with `git commit -m "a quick sentence about the changes you made"`. Make your commit messages specific, but not an entire paragraph. A sentence will do.
* **Step 4:** After you've committed a few changes (or you need to share what you have with your team) you're ready to share your new code with the world. To do that, you'll `git push origin branch-you're-on`. Always double-check on github to make sure your changes actually got pushed through accurately, and then you're good to go!

**Branches, Merges and Merge Conflicts Aren't so Scary**
