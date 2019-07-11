# Setting up, testing the kit on your machine

Here's instructions for how [our data visuals kit](https://github.com/texastribune/data-visuals-create) works and how you can get it working on your machine.

## Credentials

First thing you'll need to do is grab a few files to give you credentials to use and deploy our graphics. They will need to be given to you on a thumb drive. Take those files out of the `credentials` folder on the thumb drive and put them into your root directory. For example, on my computer it's `User/chrisessig`.

Once those on your computer, we will be creating two separate projects: one’s a graphic, another is a feature story. We’ll test both but the commands are the same.

To create a graphic, git clone our [dailies repo](https://github.com/texastribune/newsapps-dailies) and `cc` into the repo. Then run:

```sh
npx @data-visuals/create graphic test-graphic
```

To create a feature story, get out of the dailies repo and into another directory on your machine. Then run the following:

```sh
npx @data-visuals/create feature test-feature-story
```

All feature stories are placed into their our git repos under the `texastribune` account. Here's [an example](https://github.com/texastribune/feature-asset-forfeiture-2019-05).

Once the graphic and feature story are installed, [these commands](https://github.com/texastribune/data-visuals-create#available-commands) will become available to you.

You can run the following to fire up them on your localhost:

```sh
npm run serve
```

The graphic template starts empty and will remain that way until you add code. The feature article is not empty; it increase a headline, a headline, styles for the text and more.

You can also test to see if the credentials are working. The following command will deploy the project a development or a production server, depending on your settings:

```sh
npm run deploy
```

## Creating a graphic

Our graphics are embedded into stories like [this example](https://www.texastribune.org/2019/04/18/dallas-fort-worth-metro-area-saw-biggest-2018-texas-population-growth/). Now let's create one.

We use Google spreadsheets to host the data for our graphics. Here's an example of [the spreadsheet we used](https://docs.google.com/spreadsheets/d/102dLzZtUAD-kCcXIWKTnzbMM0KKhwlmE4WIVmKwSPWU/edit#gid=0) for an old graphic.

Now ahead and make a new spreadsheet and hook it up to the test graphic you created. The [readme in the create repo](https://github.com/texastribune/data-visuals-create#how-to-work-with-google-doc-and-google-sheet-files) will provide you the information you need to get this set up.

## Creating a feature story