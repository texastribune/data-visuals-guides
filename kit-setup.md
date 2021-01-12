# Setting up, testing the kit on your machine

Here's instructions for how [our data visuals kit](https://github.com/texastribune/data-visuals-create) works and how you can get it working on your machine.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Setting up, testing the kit on your machine](#setting-up-testing-the-kit-on-your-machine)
  - [Credentials](#credentials)
  - [Creating a graphic](#creating-a-graphic)
    - [Scripted VS non-scripted/static graphics](#scripted-vs-non-scriptedstatic-graphics)
    - [Fetching the data](#fetching-the-data)
    - [Creating a static graphic (HTML table)](#creating-a-static-graphic-html-table)
    - [Creating a static graphic (Illustrator)](#creating-a-static-graphic-illustrator)
    - [Creating a scripted graphic (D3)](#creating-a-scripted-graphic-d3)
  - [Creating a feature story](#creating-a-feature-story)
    - [Github](#github)
    - [Getting text on the page](#getting-text-on-the-page)
    - [Illustrator graphics and other elements](#illustrator-graphics-and-other-elements)
    - [Deploy](#deploy)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Credentials

First thing you'll need to do is get credentials for the kit. More information on this is available in the [credentials section of the computer setup readme](https://github.com/texastribune/data-visuals-guides/blob/master/computer-setup.md#credentials).

Once those on your computer, we will be creating two separate projects: one’s a graphic, another is a feature story. We’ll test both but the commands are the same.

To create a graphic, git clone our [dailies repo](https://github.com/texastribune/newsapps-dailies) and `cc` into the repo. Then run:

```sh
npx @data-visuals/create graphic test-graphic
```

To create a feature story, get out of the dailies repo and into another directory on your machine. Then run the following:

```sh
npx @data-visuals/create feature test-feature-story
```

All feature stories are placed into their own git repos under the `texastribune` account. Here's [an example](https://github.com/texastribune/feature-asset-forfeiture-2019-05).

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

One thing to note: Every time you deploy, your server will stop rendering the graphic correctly. You just need to restart the server to get it showing up again.

## Creating a graphic

### Scripted VS non-scripted/static graphics

Our graphics are embedded into stories like [this example](https://www.texastribune.org/2019/04/18/dallas-fort-worth-metro-area-saw-biggest-2018-texas-population-growth/). Now let's create one.

We have an `index.html` template, for graphics that require JavaScript, and a `static.html` template, for graphics that do not require JS.

The `index.html` is hooked up to a JS file that calls `renderGraphic()`, and in that function is where you'll put any JS needed to render the graphic,
i.e. D3. 

`static.html` does not call this function and is mainly for Illustrator embeds or HTML-only graphics, i.e. tables.

### Fetching the data

We use Google spreadsheets to host the data for our graphics. Here's an example of [the spreadsheet we used](https://docs.google.com/spreadsheets/d/102dLzZtUAD-kCcXIWKTnzbMM0KKhwlmE4WIVmKwSPWU/edit#gid=0) for an old graphic.

Now go ahead and make a new spreadsheet and hook it up to the test graphic you created. The [readme in the create repo](https://github.com/texastribune/data-visuals-create#how-to-work-with-google-doc-and-google-sheet-files) will provide you the information you need to get this set up.

Once you've created a new spreadsheet, copy over the data from [that example](https://docs.google.com/spreadsheets/d/102dLzZtUAD-kCcXIWKTnzbMM0KKhwlmE4WIVmKwSPWU/edit#gid=0). Go ahead and copy over both sheets and change their sheet names to match.

Now you can run the following to download the data:

```sh
npm run data:fetch
```

The spreadsheet will be converted into a JSON file called `data.json` and put into your `data` directory inside your graphic.

The name of the JSON file is set inside the project.config.js file. Each file in the `data` directory has its own object inside the `files` array. You can change the name of the JSON file by changing the `name` attribute.

This is useful when you want to have multiple json files for your project.

In the end, the `files` attribute inside your project.config.js should look like this. The spreadsheet ID will be found in the url.

```js
files: [
    {
      fileId: '<--Your Google spreadsheet ID here-->',
      type: 'sheet',
      name: 'data',
    },
  ],
```

### Creating a static graphic (HTML table)

Now we're going to get the data from that JSON file onto the page by recreating the table in [this project](https://github.com/texastribune/newsapps-dailies/tree/master/2019/graphic-census-data-table-2019-04). We're using [Nunjucks](https://mozilla.github.io/nunjucks/) as our templating language to make it happen.

First change the name of `app/static.html` file to `table.html`. And then make sure your `context` and `data` variables, which are at the top of the file, look like so:

```html
{# data.text --> data/text.json #}
{% set context = data.data.text %}

{# data.data --> data/data.json #}
{% set graphicData = data.data %}
```

This will put the JSON data you downloaded into a variable called `graphicData`. And `text:kv` data into the `context` variable.

And then put this inside the `<div class="app">` tag and remove `{{ prose(context.prose, context, graphicData) }}`.

```html
<p class="graphic-prose">{{ context.prose }}</p>
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
     {% for row in graphicData.datapoints %}
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
{% for row in graphicData.datapoints %}
```

We're grabbing the `graphicData` variable, which we just created and includes JSON data from our spreadsheet and looping through it, putting values from the JSON data on the page as it goes through. The `datapoints` item is a reference to the sheet name in the Google spreadsheet. It gets converted into the `data.json` file and looks like:

```js
{
  "datapoints": [
    {
      "2010": 157107,
      "2018": 222631,
      "CTYNAME": "Hays County",
      "change": 0.41706607598642964
    },
    {
      "2010": 108472,
      "2018": 148373,
      "CTYNAME": "Comal County",
      "change": 0.36784608009440223
    },
    ...
    ...
    ...
  ],
  "text": {
    "title": "Ten fastest-growing large counties in Texas from 2010 to 2018",
    "source": "U.S. Census Bureau",
    "prose": "The state’s suburban counties are home to the most rapid population growth among counties with a population equal to or greater than 20,000.",
    "credit": "Shiying Cheng"
  }
}
```

This is why we can loop through it.

Fire up your localhost if it's not already:

```sh
npm run serve
```

And open up this url in your browser:

```sh
http://localhost:3000/table/
```

And you should see your table!

### Creating a static graphic (Illustrator)

We also use Illustrator for some charts. All Illustrator files are put into the `workspace` directory.

We then use `ai2html` to convert the Illustrator file into HTML, which is exported into the `app/templates/ai2html-output/` directory (here's an [example of a project that uses an Illustator graphic](https://github.com/texastribune/newsapps-dailies/tree/master/2021/graphic-vaccine-sites-2021-01/app/templates/ai2html-output)). You can then call the Illustrator graphic(s) inside an html file in the `apps/` directory:

```js
{% set ai2html = "" %}
{% include "ai2html-output/" + ai2html + ".html" %}
```

You'll want to use the `static.html` boilerplate. (It already includes the code above for embedding an Illustrator graphic.)

### Creating a scripted graphic (D3)

We also use D3 for some of our charts. For these, it's best to start with `index.html` and add your D3 code to `renderGraphic()` in `graphic.js`.

There are several ways to import data into the JS. Go ahead and use one of the options below.

**Method 1: Use the window.DATA variable**

In the boilerplate code, you should see this:

```html
{% block inline_data %}
{% if data.data %}
<script>
  window.DATA = {{ data.data|dump }};
</script>
{% endif %}
{% endblock inline_data %}
```

This stores the `data.json` in the `data/` folder as a window variable, which you can access from your JS file with `let data = window.DATA;`.

**Method 2: Import the path to the data**

You can import your data by calling `import data from '../../data/data.json';` directly in the JS file. This path will be different if your data file is named 
something else.

**Method 3: Use loadJsonScript**

You can also use the [loadJsonScript](https://github.com/texastribune/data-visuals-create/blob/d1065320512de892f628fecb60719479774e8b2c/templates/__common__/app/scripts/utils/load-json-script.js) function to load in the data from our JSON file in the data directory.

For example, [this line chart](https://www.texastribune.org/2019/03/04/lawmakers-want-expand-dallas-teacher-incentive-pay-program/) uses D3. It's `data.json file` looks like so:

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

To import the data in the `ace` object, first add [a line like this](https://github.com/texastribune/newsapps-dailies/blob/master/2019/graphic-dallas-teacher-pay-2019-03/app/index.html#L41) to your index.html file inside the `inline_data` block:

```js
{{ data.data.ace|jsonScript('ace-data') }}
```

This will turn the data in your `data.json` file into an object on the page that can be accessed globally. Just in case you're curious, this is what the output looks like:

```html
<script id="ace-data" type="application/json">  [{"year":2015,"ace":51742.02327901564},{"year":2016,"ace":54681.095079787236},{"year":2017,"ace":56553.653136531364},{"year":2018,"ace":57983.79047619048}]
</script>
```

Then you'll import the data into the graphic.js file using the script's id tag of `ace-data`:

```js
const aceData = loadJsonScript('ace-data');
```

This will parse the data for use with D3. You can see more about how D3 charts are created by looking inside this [project's graphic.js file](https://github.com/texastribune/newsapps-dailies/blob/master/2019/graphic-dallas-teacher-pay-2019-03/app/scripts/graphic.js#L13).

## Creating a feature story

All of the commands are the same for feature stories. The difference is you start with an entire article.

We use a Google doc to house the text for feature stories. Here's a [good example of one we created for a story](https://docs.google.com/document/d/1CLKjPANEVPMOMPdjX-nrw8DetFXe__zPWeaqx8iQCZs/edit) and here's a [the feature article template](https://docs.google.com/document/d/1B_jhK1r75fMZVQev8BGU60dgjh1ffE0AxNDZz5dl-RQ/edit).

We use [archieML](http://archieml.org/) to  convert the text into JSON. Like graphics, we `data:fetch` them in the same way and the data is put into the `data/data.json` file.

### Github

One important difference between a graphic and a feature page is feature pages get their own Github repos. To do this, you will need to run the [create command](https://github.com/texastribune/data-visuals-create) outside of the `newsapps-dailies` repo. Make you include `feature` instead of `graphic` when running create. After this is run, you will then need to go to Github and create [a new repo](https://github.com/organizations/texastribune/repositories/new) inside the `texastribune` organization. Follow the instructions for setting up a Git repo inside an existing directory, which you made when you ran `create`.

Here's an example of a [final, feature repo](https://github.com/texastribune/feature-asset-forfeiture-2019-05).

### Getting text on the page

Let's create a feature article and get some text on a page! First run the `create` command to create a feature article and then go to the `project.config.js` file and change the `files` variable so it hooks up to [this Google doc](https://docs.google.com/document/d/1vIy6uXDwut2jP-kILbiM3SmECOBxZf3lPxLEtyQ_N_c/edit) we've used for a story in the past:

```js
files: [
    {
      fileId: '1vIy6uXDwut2jP-kILbiM3SmECOBxZf3lPxLEtyQ_N_c',
      type: 'doc',
      name: 'text',
    }
],
```

Now run the data fetch command. The `data/text.json` file should now look like this:

```js
{
  "title": "How the Supreme Court’s decision on the census citizenship question could affect representation in Texas",
  "seo_headline": "How a citizenship question on the U.S. Census could cost Texas",
  "pub_date": "2019-6-21",
  "authors": [
    "<a href=\"https://www.texastribune.org/about/staff/alexa-ura/\">Alexa Ura</a>",
    "<a href=\"https://www.texastribune.org/about/staff/chris-essig/\">Chris Essig</a>",
    "<a href=\"https://www.texastribune.org/about/staff/darla-cameron/\">Darla Cameron</a>"
  ],
  "parsely_authors": [
    "Alexa Ura",
    "Chris Essig",
    "Darla Cameron"
  ],
  "parsely_section": "FRONT PAGE",
  "guten_tag": "subject-redistricting",
  "summary": "The U.S. Supreme Court could soon alter the political future of Texas when it decides whether the Trump administration can ask about citizenship on the upcoming census.",
  "tweet_text": "What Texas stands to lose if the Supreme Court approves the citizenship question",
  "prose": [
    {
      "type": "text",
      "value": "The U.S. Supreme Court could soon alter the political future of Texas when it decides whether the Trump administration can ask about citizenship on the upcoming census."
    },
    {
      "type": "text",
      "value": "The administration pushed to add the question, citing it as a tool it needs to enforce the federal Voting Rights Act. But demographers and civil rights organizations have warned that immigrants and their families will be too afraid to respond to a government questionnaire that asks about citizenship status. And the U.S. Census Bureau’s own analysis shows including the question could lead to an undercount of Hispanics and noncitizens."
    },
    {
      "type": "text",
      "value": "Such an undercount in the once-a-decade census would come with serious repercussions for a state like Texas, where the number of noncitizens has helped grow the state’s political clout."
    },
    {
      "type": "insert",
      "value": {
        "align": "center",
        "illustrator": "true",
        "slug": "summary-chart"
      }
    },
    ...
    ...
    ...
    {
      "type": "correction",
      "value": "A previous version of this story included incorrect information about Congressional District 24."
    },
    {
      "type": "extra_credit",
      "value": "The code we ran for our analysis on noncitizens in Texas’ political districts is available on <a href=\"https://github.com/texastribune/scotus-citizenship-analysis\">Github</a>."
    }
  ]
}
```

You'll notice that text for our story is given the `type` of `text`, which will be important later.

Now go to your index.html file. You'll notice this line:

```html
{{ prose(context.prose, context, featureData) }}
```

This calls the `prose` macro within the [app/templates/macros/prose.html file](https://github.com/texastribune/data-visuals-create/blob/master/templates/__common__/app/templates/macros/prose.html) and loops through all lines in your `text.json` file, putting each on the page.

To do this, the `prose` macro calls another macro within the [app/templates/macros/processors.html file](https://github.com/texastribune/data-visuals-create/blob/master/templates/feature/app/templates/macros/processors.html). It picks out the appropriate macro depending on what type of content is being looped through. For instance, since the story's paragraphs has a type of `text` in the `data.json` file, it's passed to this macro:

```
{% macro text(value, context, data) %}
  <p class="copy">{{ value | renderStringWithNunjucks(data) }}</p>
{% endmacro %}
```

The result is the paragraph is wrapped in a `<p class="copy">` tag and placed on the page. It does this over and over, until all the text is placed on the page.

### Illustrator graphics and other elements

Charts and other elements are placed on the page differently than they are in graphic projects. You will notice in [this example](https://docs.google.com/document/d/1vIy6uXDwut2jP-kILbiM3SmECOBxZf3lPxLEtyQ_N_c/edit), one of our Illustrator graphics is inserted into the Google doc like so:

```html
{.insert}
align: center
illustrator: true
slug: summary-chart
{}
```

When it's converted into the `text.json` file, it looks like:

```js
{
  ...
  ...
  ...
  "prose": [
    ...
    ...
    ...
    {
      "type": "insert",
      "value": {
        "align": "center",
        "illustrator": "true",
        "slug": "summary-chart"
      }
    },
    ...
    ...
    ...
  ]
}
```

You'll then place that on the page using the same `processors.html` file from before. Only we will need to add a new macro to handle content with the type of `insert`.

```html
{% macro insert(value) %}
  {% include "ai2html-output/" + value.slug + ".html" %}
{% endmacro %}
```

Here's a more complicated example from [this story](https://github.com/texastribune/feature-scotus-citizenship-2019-06/blob/master/app/templates/macros/processors.html).

### Deploy

Once you are ready for the story to go live, make sure you change the `bucket` in the `project.config.js` from moose to apps. Here's what it [should look like](https://github.com/texastribune/feature-asset-forfeiture-2019-05/blob/master/project.config.js#L14) when you're done.

