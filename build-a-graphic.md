#So you want to build a graphic...

A reporter probably came over a minute ago and said something like 'I have a spreadsheet of xyz and I would like a map please'. Cool! This will help you get your graphic started- but it will **not** help you build a map. 

##[newsapps-dailies](https://github.com/texastribune/newsapps-dailies)

This is where all of the news apps dailies live. The first step is to create a branch for your new project and create a new project folder on that branch. It's a good idea to try to call it the slug of the project you're working on- but if you don't know that yet it's okay to guess.

##[newsapps-graphics-kit](https://github.com/texastribune/newsapps-graphic-kit)

This is the generator for all of our graphics. You'll use this for pretty much everything- unless you're making a huge app in which case you'll use the Apps Kit. Clone this onto your desktop or into your trib folder so you don't have to dig for it every time you start a project.

Copy the contents of this folder into your new project folder in newsapps-dailies. Delete the `.git` folder in there, so github doesn't get mad (github will make a new git folder when you push your folder up with the newsapps-dailies). If you don't know how to find hidden files, follow [this tutorial](http://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/).

Follow the [READ-ME](https://github.com/texastribune/newsapps-graphic-kit/blob/master/README.md) in the graphics kit to get started. You're already on your way!

##Make a story page in the CMS

Sign into the cms and click on 'Stories' in the 'Content' section. Make sure the reporter hasn't already created a story page by either asking them (duh) or looking through the listed stories- they're listed chronalogically. Otherwise, click 'Add Story'. Do the normal stuff: add authors (usually news apps team goes after reporters), publication status is usually draft and find out the publish data from the editor.

The homepage headline and SEO headline will probably be changed by the editor- but put your best guess in there so the reporter can easily find it later. It's usually best to wait until the reporter has put text into the body section and has told you where they want your graphic to go because they'll probably overwrite it. If they haven't yet or you just want to see what it looks like- that's okay too. You'll probably just have to re-add it in later.

Go to your /preview page for the graphic you're working on (probably [http://localhost:3000/preview.html](http://localhost:3000/preview.html) unless you're running form a different port) and grab the HTML embed link near the bottom of the page just below your graphic.

Open the HTML editor on the body text (literally a button that says HTML in the editor bar) and paste that HTML snippet wherever the reporter/editor/you want it to go. That is where your graphic will appear in the story page.