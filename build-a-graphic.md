#So you want to build a graphic...

A reporter probably came over a minute ago and said something like 'I have a spreadsheet of xyz and I would like a map please'. Cool! This will help you get your graphic started- but it will **not** help you build a map. 

##First thing's first:

Check with the editor to make sure they know what's up. Get a run date and give them an idea of what you'll be working on. Be sure to inform Art of what you're up to and ask for lead art. **Do this in the very beginning** lest they murder you for keeping them late to make you a stupid collage.

##[newsapps-dailies](https://github.com/texastribune/newsapps-dailies)

This is where all of the news apps dailies live. The first step is to create a branch for your new project and create a new project folder on that branch. It's a good idea to try to call it the slug of the project you're working on- but if you don't know that yet it's okay to guess.

##[newsapps-graphics-kit](https://github.com/texastribune/newsapps-graphic-kit)

This is the generator for all of our graphics. You'll use this for pretty much everything- unless you're making a huge app in which case you'll use the [newsapps-app-kit](https://github.com/texastribune/newsapps-app-kit). Clone this onto your desktop or into your trib folder so you don't have to dig for it every time you start a project.

Copy the contents of this folder into your new project folder in newsapps-dailies. Delete the `.git` folder in there, so github doesn't get mad (github will make a new git folder when you push your folder up with the newsapps-dailies). If you don't know how to find hidden files, follow [this tutorial](http://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/).

Follow the [READ-ME](https://github.com/texastribune/newsapps-graphic-kit/blob/master/README.md) in the graphics kit to get started. You're already on your way!

##Make sure it works.

Check your graphic on Firefox, Chrome and Safari. Then **check it on your phone**. 

##Make a story page in the CMS

So you've finished the hard part and are ready to put your graphic into a story page in the CMS.

Sign into the CMS and click on 'Stories' in the 'Content' section. Make sure the reporter hasn't already created a story page by either asking them (duh) or looking through the listed stories- they're listed chronalogically. Otherwise, click 'Add Story'. 

Do the normal stuff: add authors (usually reporters go first), publication status is draft and find out the publish date from the editor.

![the basics](http://i.imgur.com/5K9QrfG.png)

The homepage headline and SEO headline will probably be changed by the editor- but put your best guess in there so the reporter can easily find it later. It's usually best to wait until the reporter has put text into the body section and has told you where they want your graphic to go because they'll probably overwrite it. If they haven't yet or you just want to see what it looks like- that's okay too. You'll probably just have to re-add it in later.

![story detail section](http://i.imgur.com/lQfhQbS.png)

Go to your /preview.html page for the graphic you're working on (probably [http://localhost:3000/preview.html](http://localhost:3000/preview.html) unless you're running from a different port) and grab the HTML embed link near the bottom of the page just below your graphic. We use [Pym.js](http://blog.apps.npr.org/pym.js/) which puts our graphics into responsive iframes that are embedded into the story pages.

Open the HTML editor on the body text (literally a button that says HTML in the editor bar) and paste that HTML snippet wherever the reporter/editor/you want it to go. That is where your graphic will appear in the story page.

The short summary and long summaries are what will appear in social cards and on the home page. More often than not it will closely resemble the first couple sentences of the story. 

Remember that lead art you asked so nicely for? It's time to use it! Click the magnifying glass and look for your art. These are also listed chronologically so it'll probably be near the top.

![lead art](http://i.imgur.com/yq8rTT3.png)

*Add tags.* This is important. Front page, politics, and the obvious other topics. Be generous with tags.

*Add news apps tribpedia* so it'll show up in our [tribpedia page](http://www.texastribune.org/tribpedia/newsapps/).

![tags and tribpedia entries](http://i.imgur.com/qMs4Tp3.png)

Open the *Advanced Options* section and scroll down to the HTML embed field.

![advanced options](http://i.imgur.com/0ArGcIw.png)

Copy and paste the second bit of code at the bottom of [http://localhost:3000/preview.html](http://localhost:3000/preview.html) into that section. This is what activates [Pym.js](http://blog.apps.npr.org/pym.js/) and adjusts the height of the iframe you put into the story whenever the page (or your graphic) resizes.

![advanced options expanded](http://i.imgur.com/9AWbD8T.png)

Click the ![Save and continue editing](http://i.imgur.com/9biiKWw.png) button at the top and then 'view on site'. You should see your graphic on the page in the story.

And of course, **CHECK ON FIREFOX, CHROME AND SAFARI. THEN CHECK IT ON YOUR PHONE.** Make sure all assets are loading correctly and it's not getting cut off at the bottom.

