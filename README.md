# Texas Tribune Data Visuals Guides

Here you will find a collection of guides for doing various Data Visuals tasks. Find yourself needing to describe how to setup something for a project? Try to document it here instead so it can be linked to later!

## [Set up your news apps computer environment](computer-setup.md)

There are a few things we have to do to get your computer ready for all the cool stuff you're going to build.

## [Set up our explorers on your computer](explorers-setup.md)

Here's how you get specific explorers set up on your computer

## [Setting up, testing the kit on your machine](kit-setup.md)

Here's how to set up and deploy your first projects

## [Setting up geo software on our your computer](geo-setup.md)

This is specifically aimed at geo software

## Decision Tree

We have four ways of making graphics: 
1. DataWrapper charts embedded in stories via the graphics plugin [Example](https://www.texastribune.org/2021/05/23/texas-voting-polling-restrictions/)
	- Upside: Easy to make, quick turnaround, accessible, not too difficult to make one or two quick updates.
	- Downside: Limited to their chart types, a bit less room to be creative or introduce interactivity. Needs further integration with our CMS as of spring 2021, hard to maintain templates separate from Queso.
2. ai2html graphics published with the kit and embedded in stories via the graphics plugin [Example](https://www.texastribune.org/2021/05/23/texas-voting-polling-restrictions/)
	- Upside: High production value, very customizable for chart shapes that DataWrapper cannot handle. 
	- Downside: Less responsive, not interactive, learning curve for Illustrator can be high, hard to maintain templates separate from Queso, bad for something that needs frequent updates.  
3. Coded graphics embedded in stories [Example](https://www.texastribune.org/2021/04/26/texas-congress-seats-gain/)
	- Upside: Entirely customizable, can include limited interactivity like a dropdown or address lookup. Enables d3 and automation for charts that have to update more than once or twice.
	- Downside: Harder to polish styles, more code to write for responsiveness, learning curve for D3 or other coded elements can be high. Need to build more accessibility into our system.  
4. Apps page feature stories, which are deployed separately. [Example](https://apps.texastribune.org/features/2020/texas-coronavirus-cases-map/)
	- Upside: A sandbox to do whatever we want, infinitely flexible. Can customize elements of the story beyond charts with address lookups etc. Can incorporate scraping for easy frequent updates. 
	- Downside: worse SEO performance than CMS stories, harder to use images without the built-in processing tools from the CMS, much harder to get out the door.

## License

All guides are licensed under a [Creative Commons BY-NC 4.0](http://creativecommons.org/licenses/by-nc/4.0/) license.
