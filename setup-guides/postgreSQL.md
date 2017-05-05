## Installing PostgreSQL

Nearly all of our projects use [PostgreSQL](http://www.postgresql.org/) as their backend. Instead of installing it with Homebrew, we use [Postgres.app](http://postgresapp.com/) instead.

Visit [http://postgresapp.com/](http://postgresapp.com/) and download the installer. After installing, run the app. You should get a pop up window and see a cute little elephant romping around in your menu bar in the top right. If you see the elephant, Postgres.app is live.

Next we need to add Postgres.app's folder to our `$PATH` so our terminal can find the PostgreSQL commands. We will do this in our `.bash_profile`.

> Note: This line needs to come **before** what we added for Homebrew. Otherwise, Homebrew's `brew doctor` will throw a fit. This is to ensure that command added by Homebrew are seen before the PostgreSQL commands.

Add this line to the top, then `source .bash_profile`:

`export PATH=/Applications/Postgres.app/Contents/Versions/latest/bin:$PATH`

Run `which psql` in your terminal to make sure your computer recognizes your changes.