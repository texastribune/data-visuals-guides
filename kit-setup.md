# Setting up, testing the kit on your machine

Here's instructions for how [our data visuals kit](https://github.com/texastribune/data-visuals-create) works and how you can get it working on your machine.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Credentials](#credentials)
- [Creating a graphic](#creating-a-graphic)
- [Creating a feature story](#creating-a-feature-story)

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

#### Nunjucks

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

## Creating a feature story