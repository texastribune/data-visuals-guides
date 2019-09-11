# Set up our explorers on your computer

Here's a list up all the explorers and apps we maintain, along with setup instructions for each. Most of these are documented in other locations. This doc attempts to gather all those links into one place.

This assumes that everything in the [computer setup](computer-setup.md) section has been installed.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Salaries](#salaries)
- [Prisons](#prisons)
- [Schools](#schools)
- [Republic API](#republic-api)
  - [Cloud SQL proxy](#cloud-sql-proxy)
  - [FAQ](#faq)
- [Campaign finance](#campaign-finance)
- [Elections](#elections)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## [Salaries](https://salaries.texastribune.org/)

The basic setup is documented on in its [Github repo](https://github.com/texastribune/salaries.texastribune.org).

How to update salaries in [documented on Confluence](https://wiki.texastribune.org/pages/viewpage.action?pageId=12420703).

You will need to SSH into the production server in order to update the DB. You will first need to create a `~/.ssh/config` file if you don't have one already.

Then, scroll to the bottom of this [Confluence readme](https://wiki.texastribune.org/display/TECH/AWS+hosts) and paste the `Host proxy` and `Host salaries-prod-2` blocks into your `config` file. You can create these blocks for other commands with the info in the table. 

As part of the setup, you will need to get the `newsapps.pem` and `tribtalk-kp.pem` keyfiles, which we can hook you up with. After you get the keys, you'll need to add them to the path `~/.ssh/trib/`. You can do this by running `cd ~/.ssh/trib/`, `open .`, and then dragging the key files into the Finder window.

Now run `ssh salaries-prod-2`. If you are getting the error `ssh_exchange_identification: Connection closed by remote host`, there may be a problem with your key file. Run `chmod 600 tribtalk.pem` in the `trib/` folder to remove some permissions from the keyfile, and try `ssh salaries-prod-2` again. (The `salaries-prod-2` command relies on the `ssh proxy` command, which relies on the `tribtalk.pem` key file ⁠— it doesn't like key files that are too open.)

## [Prisons](https://www.texastribune.org/library/data/texas-prisons/)

Prisons is in the Github repo for the Tribune's main site. It's updated once a month. We've documented how to update in [this readme](https://github.com/texastribune/texastribune/tree/master/snollygoster/dataapps/prisons/scripts).

To deploy to the production DB, you will need to get credentials for the Tribune site. Currently, Daniel is the one responsible for handing those out.

## [Schools](https://schools.texastribune.org/)

The schools app is updated once a year, using new data from the government. The code behind the app is located in this [Github repo](https://github.com/texastribune/scuole). The data is loaded separately in [this repo](https://github.com/texastribune/scuole-data/).

To get this set up locally, you'll need to create a new directory on your machine. Then clone both of those directories into the directory you created.

Next you'll need to want to create a `.env` file in the `scuole` directory. You'll want to include the following line:

```sh
export DATA_FOLDER=/Users/chrisessig/Documents/tribune/github/scuole-house/scuole-data/
```

Make sure you change the location to match the directory of `scuole-data` on your machine.

Once this is completed, you should be able to start running make commands. Some of these are documented in the [scuole readme](https://github.com/texastribune/scuole).

To `ssh` into the schools production database, follow the same instructions for the salaries database but replace `salaries-prod-2` with `schools-prod`.

## [Republic API](https://republic.texastribune.org/api/v1/)

This is the API that powers our directory, as well election results. Basic setup information is located in it's [Github repo](https://github.com/texastribune/republic).

Once you are have this downloaded and the `pipenv` environment set up, you have several [make commands](https://github.com/texastribune/republic/blob/master/Makefile) at your disposal.

To deploy any changes to production, you will need to be added to our `data-visuals` project on the [Google Cloud Platform](https://console.cloud.google.com/home/dashboard?project=data-visuals-161818). Daniel can get you set up with this.

Then you will need to install the Cloud SDK. Instructions for Mac users is available on [this Google Cloud](https://cloud.google.com/sdk/docs/quickstart-macos) page.

Once installed, you can run the following to get credentials installed to `gcloud`:

```sh
gcloud init
```

Make sure when it's time to pick a project, you pick the one that starts with `data-visuals`.

### Cloud SQL proxy

You may run into isses getting the server to work on your local machine. If so, go to your `/etc/hosts` file and add the following to the bottom of the file:

```sh
127.0.0.1 local.texastribune.org
```

### FAQ

We have also created a FAQ page on Confluence for [documenting random issues](https://wiki.texastribune.org/display/APPS/Republic+API+FAQ) we run into with the API.

## [Campaign finance](https://github.com/texastribune/campaign-finance-viewer_)

We have an app for downloading campaign finance data from the state. More information on how it works, as well as resources for federal campaign finance data, can be found on [this Confluence page](https://wiki.texastribune.org/display/APPS/Ryan's+Brain#Ryan'sBrain-CampaignFinance).

The [readme](https://github.com/texastribune/campaign-finance-viewer/blob/master/README.md) also has commands for setting it up on your machine.

## [Elections](https://apps.texastribune.org/elections/2018/texas-midterm-election-results)

These [scripts will pull](https://github.com/texastribune/sos-collector) election results from the Secretary of State. We also have a little bit of documention on election night on [this Confluence page](https://wiki.texastribune.org/display/APPS/Ryan's+Brain#Ryan'sBrain-ElectionNight).

More information on how to work with election results, as well as plans for the next election cycle, is documented in [this Google doc](https://docs.google.com/document/d/1UaUfQKH01QucTewv2p9fuQRx6JCO90PGaik91JilMZM/edit#heading=h.x2ziamsevlx).
