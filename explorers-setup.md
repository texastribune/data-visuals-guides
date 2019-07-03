# Set up our explorers on your computer

Here's a list up all the explorers and apps we maintain, along with setup instructions for each. Most of these are documented in other locations. This doc attempts to gather all those links into one place.

This assumes that everything in the [computer setup](computer-setup.md) section has been installed.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Salaries](#salaries)
- [Prisons](#prisons)
- [Schools](#schools)
- [Republic API](#republic-api)
- [Campaign finance](#campaign-finance)
- [Elections](#elections)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## [Salaries](https://salaries.texastribune.org/)

The basic setup is documented on in its [Github repo](https://github.com/texastribune/salaries.texastribune.org).

How to update salaries in [documented on Confluence](https://wiki.texastribune.org/pages/viewpage.action?pageId=12420703).

You will need to SSH into the production server in order to update the DB. You will first need to create a `~/.ssh/config` file if you don't have one already. And then copy the salaries production info shown at the bottom of this [Confluence readme](https://wiki.texastribune.org/display/TECH/AWS+hosts0).

As part of the setup, you will need to get a `newsapps.pem` file, which we can hook you up with.

## [Prisons](https://www.texastribune.org/library/data/texas-prisons/)

Prisons is in the Github repo for the Tribune's main site. It's updated once a month. We've documented how to update in [this readme](https://github.com/texastribune/texastribune/tree/master/snollygoster/dataapps/prisons/scripts).

To deploy to the production DB, you will need to get credentials for the Tribune site. Currently, Daniel is the one responsible for handing those out.

## [Schools](https://schools.texastribune.org/)

The schools app is updated once a year, using new data from the government. The code behind the app is located in this [Github repo](https://github.com/texastribune/scuole). The data is loaded separately in [this repo](https://github.com/texastribune/scuole-data/).

This section will be more fleshed out next time we update schools.

## [Republic API](https://republic.texastribune.org/api/v1/)

This is the API that powers our directory, as well election results. Basic setup information is located in it's [Github repo](https://github.com/texastribune/republic).

Once you are have this downloaded and the `pipenv` environment set up, you have several [make commands](https://github.com/texastribune/republic/blob/master/Makefile) at your disposal.

For instance, you can run:

```sh
make init_db
```

To get a database set up locally. As of right now, the database is called `tt_dev2_republic_v2`.

To deploy any changes to production, you will need to be added to our `data-visuals` project on the [Google Cloud Platform](https://console.cloud.google.com/home/dashboard?project=data-visuals-161818). Daniel can get you set up with this.

Then you will need to install the Cloud SDK. Instructions for Mac users is available on [this Google Cloud](https://cloud.google.com/sdk/docs/quickstart-macos) page.

Once installed, you can run the following to get credentials installed to `gcloud`:

```sh
gcloud init
```

Make sure when it's time to pick a project, you pick the one that starts with `data-visuals`.

### Cloud SQL proxy

We use a cloud sql proxy to open a connection locally to the production database. You will need to install the proxy client using [these instructions](https://cloud.google.com/sql/docs/postgres/quickstart-proxy-test).

Once you've installed the proxy, go to [this page](https://console.cloud.google.com/sql/instances/data-visuals-db/overview?project=data-visuals-161818&duration=PT1H) and copy the `Instance connection name` for the database.

Copy that instance name and run the following command with it:

```sh
./cloud_sql_proxy -instances=<INSTANCE_CONNECTION_NAME>=tcp:5432
```

This will open a proxy. Now open a new tab in your terminal and run the following to get the production database running on your local machine:

```sh
python manage.py runserver
```

You can run the following to start editing the data on the production database:

```sh
python manage.py shell_plus
```

Right now, we create lawmakers using the [following commands](https://github.com/texastribune/republic/blob/master/CREATING_OFFICEHOLDERS.md).

A few more details on how this works is available in [this Google doc](https://docs.google.com/document/d/1UaUfQKH01QucTewv2p9fuQRx6JCO90PGaik91JilMZM/edit#), which a transcript of a Slack conversation between Chris and Ryan shortly after Ryan left.

## Campaign finance

We have an app for [downloading campaign finance data](https://github.com/texastribune/campaign-finance-viewer) from the state. More information on how it works, as well as resources for federal campaign finance data, can be found on [this Confluence page](https://wiki.texastribune.org/display/APPS/Ryan's+Brain#Ryan'sBrain-CampaignFinance).

This section will be more fleshed out as we begin using the app more and more.

## [Elections](https://apps.texastribune.org/elections/2018/texas-midterm-election-results)

These [scripts will pull](https://github.com/texastribune/sos-collector) election results from the Secretary of State. We also have a little bit of documention on election night on [this Confluence page](https://wiki.texastribune.org/display/APPS/Ryan's+Brain#Ryan'sBrain-ElectionNight).

More information on how to work with election results, as well as plans for the next election cycle, is documented in [this Google doc](https://docs.google.com/document/d/1UaUfQKH01QucTewv2p9fuQRx6JCO90PGaik91JilMZM/edit#heading=h.x2ziamsevlx).

This section will be more fleshed out as we get closer to the next elections.


