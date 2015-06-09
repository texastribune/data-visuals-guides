#So you want to build a graphic...

A reporter probably came over a minute ago and said something like 'I have a spreadsheet of xyz. Can we make something out of it?'. Yay! This guide will show you how to create a graphic from start to publish.

_This guide also assumes you know basic terminal commands (`cd`, `ls`, etc.) and that you understand the Github tutorial._

##First thing's first:

Check with the editor to make sure they know what's up. Get a run date and give them an idea of what you'll be working on. Be sure to inform Art of what you're up to and ask for lead art. **Do this in the very beginning** lest they murder you for keeping them late to make you a stupid collage. Not that any of us have ever done that...

##[newsapps-dailies](https://github.com/texastribune/newsapps-dailies)

This is where all of the news apps dailies live. The first step is to create a branch for your new project and create a new project folder on that branch. It's a good idea to try to call it the slug of the project you're working on- but if you don't know that yet, it's okay to guess.

##[newsapps-graphics-kit](https://github.com/texastribune/newsapps-graphic-kit)

This is the generator for all of our graphics. You'll use this for pretty much all of the smaller daily graphics you'll build. Sometimes we build bigger, [way](http://apps.texastribune.org/shale-life/) [cool](http://apps.texastribune.org/blood-lessons/) [apps](http://apps.texastribune.org/hurting-for-work/), in which case you'll use the [newsapps-app-kit](https://github.com/texastribune/newsapps-app-kit). Clone the [graphics kit](https://github.com/texastribune/newsapps-graphic-kit) onto your desktop or into your trib folder so you don't have to dig for it every time you start a project.

Copy the contents of the graphics kit into your new project folder you created in newsapps-dailies. Delete the `.git` folder in there, so github doesn't get mad (github will make a new git folder when you push your folder up with the newsapps-dailies). If you don't know how to find hidden files, follow [this tutorial](http://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/).

Follow the [READ-ME](https://github.com/texastribune/newsapps-graphic-kit/blob/master/README.md) in the graphics kit to get started and get to work!

###Fun things about our Graphics Kit

You will rarely need to add any kind of padding. You'll notice as you're building that the graphic will sit right on the edge of the browser window- this is okay. You will be tempted to add some kind of padding or margin to the outside- don't. It'll be put in an iframe later.

If your graphic is going into a story page (which if you're reading this, it probably is) it will never appear wider than 670px so don't worry about designing beyond that width.

Our graphics kit comes with a way cool /preview.html page (probably [http://localhost:3000/preview.html](http://localhost:3000/preview.html) unless you're running from a different port) you can check out to see your graphic as the widths it'll be in our story page as well as a mobile width. At the bottom, it also has some handy code snippets you'll need when you're publishing. 

##Make sure it works.

After you've finished your graphic, pushed it up to github, and ran your `gulp build` and `npm run deploy`, check your graphic on Firefox, Chrome and Safari. Then **check it on your phone**. 

##Make a story page in the CMS

So you've finished building your beautiful graphic and are ready to put it into a story page in the CMS.

Sign into the CMS and click on 'Stories' in the 'Content' section. Make sure the reporter hasn't already created a story page by either asking them (duh) or looking through the listed stories- they're listed chronalogically so it should be near the top. Otherwise, click 'Add Story'. 

Do the normal stuff: add authors (usually reporters go first), publication status is draft and find out the publish date/time from the editor.

![the basics](http://i.imgur.com/5K9QrfG.png)

The homepage headline and SEO headline will probably be changed by the editor- but put your best guess in there so the reporter can easily find it later. As for placing your graphic, it's usually best to wait until the reporter has put text into the body section and has told you where they want your graphic to go because they'll probably overwrite it. If they haven't yet or you just want to see what it looks like- that's okay too. You'll probably just have to re-add it in later.

![story detail section](http://i.imgur.com/lQfhQbS.png)

We use [Pym.js](http://blog.apps.npr.org/pym.js/) which puts our graphics into responsive iframes that are embedded into the story pages. To make that work, go to your /preview.html page for the graphic you're working on and grab the HTML embed link near the bottom of the page just below your graphic. 

Open the HTML editor on the body text (literally a button that says HTML in the editor bar) and paste that HTML snippet wherever the reporter/editor/you wants it to go in the story. That is where your graphic will appear in the story page.

The short summary and long summaries are what will appear in social cards and on the home page. More often than not it will closely resemble the first couple sentences of the story. 

Remember that lead art you asked so nicely for? It's time to use it! Click the magnifying glass and look for your art. These are also listed chronologically so it'll probably be near the top.

![lead art](http://i.imgur.com/yq8rTT3.png)

*Add tags.* This is important. Front page, politics, and the obvious other topics. Be generous with tags.

*Add news apps tribpedia* so it'll show up in our [tribpedia page](http://www.texastribune.org/tribpedia/newsapps/) and people can find your cool stuff.

![tags and tribpedia entries](http://i.imgur.com/qMs4Tp3.png)

Open the **Advanced Options** section and scroll down to the HTML embed field.

![advanced options](http://i.imgur.com/0ArGcIw.png)

Copy and paste the second bit of code at the bottom of [http://localhost:3000/preview.html](http://localhost:3000/preview.html) into that section. This is what activates that [Pym.js](http://blog.apps.npr.org/pym.js/) we were talking about earlier and adjusts the height of the iframe you put into the story whenever the page (and, consequently, your graphic) resizes.

![advanced options expanded](http://i.imgur.com/9AWbD8T.png)

Click the ![Save and continue editing](http://i.imgur.com/9biiKWw.png) button at the top and then 'view on site'. You should see your graphic on the page in the story.

And of course, **CHECK ON FIREFOX, CHROME AND SAFARI. THEN CHECK IT ON YOUR PHONE.** Make sure all assets are loading correctly and it's not getting cut off at the bottom. 

Send the preview link to at least a few people on the news apps team to get some extra eys on it and have them test it on their devices. Then send it to the editor and reporter on the case to get their approval.

If your story is set to publish the next morning, be sure to **bring your computer home**. It's not unlikely to get a few last-minute tweaks the night before.
