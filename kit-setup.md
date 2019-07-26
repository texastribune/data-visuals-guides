# Setting up, testing the kit on your machine

Here's instructions for how [our data visuals kit](https://github.com/texastribune/data-visuals-create) works and how you can get it working on your machine.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Credentials](#credentials)
- [Creating a graphic](#creating-a-graphic)
  - [Nunjucks](#nunjucks)
  - [Other chart types](#other-chart-types)
    - [D3](#d3)
    - [Illustrator](#illustrator)
- [Creating a feature story](#creating-a-feature-story)
    - [Github](#github)
    - [Deploy](#deploy)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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

Once you've created a new spreadsheet, copy over the data from [that example](https://docs.google.com/spreadsheets/d/102dLzZtUAD-kCcXIWKTnzbMM0KKhwlmE4WIVmKwSPWU/edit#gid=0). Go ahead and copy over both sheets and change their sheet names to match.

Now you can run the following to download the data:

```sh
npm run data:fetch
```

The spreadsheet will be converted into a json file called `data.json` and put into your `data` directory inside your graphic.

The name of the json file is set inside the project.config.js file. Each file in the `data` directory has its own object inside the `files` array. You can change the name of the json file by changing the `name` attribute.

This is useful when you want to have multiple json files for your project. 

### Nunjucks

Now we're going to get the data from that json file onto the page by recreating the table in [this project](https://github.com/texastribune/newsapps-dailies/blob/master/graphic-census-data-table-2019-04/app/index.html). We're using [Nunjucks](https://mozilla.github.io/nunjucks/) as our templating language to make it happen.

First you'll go into your `app/index.html` file and add the following near the top of the page (but under `base.html`):

```html
{% set context = data.data %}
```

This will put the json data you downloaded into a variable called `context`.

And then put this inside the `<div class="app">` tag:

```html
<table class="dv-table">
  <thead>
    <tr> 
      <th>County</th>
      <th class="number">2010 pop. </th>
      <th class="number">2018 pop. </th>
      <th class="number">Percent change</th>
    </tr>
  </thead>
  <tbody>
     {% for row in context.datapoints %}
       <tr>
        <td> {{ row.CTYNAME }} </td>
        <td class="number"> {{ row["2010"] | intcomma }} </td>
        <td class="number"> {{ row["2018"] | intcomma }} </td>
        <td class="percent"> +{{ (row.change * 100) | round(2) }}%</td>
      </tr>
    {% endfor %}
  </tbody>
</table>
```

You'll notice that this includes the following for loop:

```html
{% for row in context.datapoints %}
```

We're grabbing the `context` variable, which we just created and includes json data from our spreadsheet and looping through it, putting values from the json data on the page as it goes through. The `datapoints` item is a reference to the sheet name in the Google spreadsheet. It gets converted into the `data.json` file and looks like:

```js
{
  "datapoints": [
    {
      "2010": 82,
      "2018": 152,
      "CTYNAME": "Loving County",
      "change": 0.8536585365853658
    },
    {
      "2010": 157107,
      "2018": 222631,
      "CTYNAME": "Hays County",
      "change": 0.41706607598642964
    },
    ...
    ...
    ...
  ],
  "text": {
    "title": "headline",
    "source": "U.S. Census Bureau",
    "prose": "graphic_prose",
    "credit": "Shiying Cheng"
  }
}
```

This is why we can loop through it.

Fire up your localhost if it's not already. And you should a table!

### Other chart types

#### D3

We also use D3 for some of our charts. For these, you will be using the [loadJsonScript](https://github.com/texastribune/newsapps-dailies/blob/master/graphic-dallas-teacher-pay-2019-03/app/scripts/utils/load-json-script.js) to load in the data from our json file in the data directory.

For example, [this line chart](https://www.texastribune.org/2019/04/18/dallas-fort-worth-metro-area-saw-biggest-2018-texas-population-growth/) uses D3. It's `data.json file` looks like so:

```js
{
  "ace": [
    {
      "year": 2015,
      "ace": 51742.02327901564
    },
    {
      "year": 2016,
      "ace": 54681.095079787236
    },
    {
      "year": 2017,
      "ace": 56553.653136531364
    },
    {
      "year": 2018,
      "ace": 57983.79047619048
    }
  ...
  ...
  ...
  ],
  "text": {
    "title": "Dallas ISD incentivized higher-rated teachers to work at low-performing schools",
    "source": "Texas Education Agency",
    "prose": "At Dallas ISD, higher-rated teachers make more money. When the district implemented the first iteration of the Accelerating Campus Excellence, also known as ACE,  program at seven schools in 2015-16, bonuses helped lure more higher-paid teachers to those underperforming schools.",
    "credit": "Shiying Cheng",
    "note": ""
  }
}
```

And it's imported into the graphic.js file doing:

```js
const aceData = loadJsonScript('ace-data');
```

You can see more about how D3 charts are created by looking inside this [project's graphic.js file](https://github.com/texastribune/newsapps-dailies/blob/master/graphic-dallas-teacher-pay-2019-03/app/scripts/graphic.js).


#### Illustrator

We also use Illustrator for some charts. All Illustrator files are put into the [workspace directory](https://github.com/texastribune/newsapps-dailies/tree/master/graphic-census-data-table-2019-04/workspace).

We then use `ai2html` to convert the Illustrator file into HTML, which is exported into [app/templates/ai2html-output/ directory](https://github.com/texastribune/newsapps-dailies/tree/master/graphic-census-data-table-2019-04/app/templates/ai2html-output). You can then [call the Illustrator graphic(s)](https://github.com/texastribune/newsapps-dailies/blob/master/graphic-census-data-table-2019-04/app/map.html#L7) inside an html file in the `apps/` direcotry. 

```html
<div id="graphic-budget-scraps" class="graphic app">
  {% set ai2html = "census-map" %}
  {% include "ai2html-output/" + ai2html + ".html" %}
</div>
```

## Creating a feature story

All of the commands are the same for feature stories. The difference is you start with an entire article.

We use a Google doc to house the text for feature stories. Here's a [good example of one we created for a story](https://docs.google.com/document/d/1CLKjPANEVPMOMPdjX-nrw8DetFXe__zPWeaqx8iQCZs/edit) and here's a [the feature article template](https://docs.google.com/document/d/1B_jhK1r75fMZVQev8BGU60dgjh1ffE0AxNDZz5dl-RQ/edit).

We use `archieML` to  convert the text into json. Like graphics, we `data:fetch` them in the same way and the data is put into the `data/data.json` file.

#### Github

One important difference between a graphic and a feature page is feature pages get their own Github repos. To do this, you will need to run the [create command](https://github.com/texastribune/data-visuals-create) outside of the `newsapps-dailies` repo. Make you include `feature` instead of `graphic` when running create. After this is run, you will then need to go to Github and create [a new repo](https://github.com/organizations/texastribune/repositories/new) inside the `texastribune` organization. Follow the instructions for setting up a Git repo inside an existing directory, which you made when you ran `create`.

Here's an example of a [final, feature repo](https://github.com/texastribune/feature-asset-forfeiture-2019-05).

#### Deploy

Once you are ready for the story to go live, make sure you change the `bucket` in the `project.config.js` from moose to apps. Here's what it [should look like](https://github.com/texastribune/feature-asset-forfeiture-2019-05/blob/master/project.config.js#L14) when you're done.

