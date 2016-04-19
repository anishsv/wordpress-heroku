# WordPress Heroku

This project is a guide for deploying [WordPress](http://wordpress.org/) on [Heroku](http://www.heroku.com/). The repository comes bundled with:
* [PostgreSQL for WordPress](http://wordpress.org/extend/plugins/postgresql-for-wordpress/)

## Installation

Clone the repository from Github

    $ git clone  https://github.com/anishsv/wordpress-heroku.git

With the [Heroku gem](http://devcenter.heroku.com/articles/heroku-command), create your app

    $ cd wordpress-heroku
    $ heroku create
      Creating app... done, stack is cedar-14
      https://your-app-url.herokuapp.com/ | https://git.heroku.com/your-app-url.git

Add a database to your app

    $ heroku addons:create heroku-postgresql
      Creating HEROKU_POSTGRESQL_INSTANCE... done, (free)
      Adding HEROKU_POSTGRESQL_INSTANCE to your-app-url... done
      Setting DATABASE_URL and restarting your-app-url... done, v3
      Database has been created and is available
       ! This database is empty. If upgrading, you can transfer
       ! data from another database with pg:copy
      Use `heroku addons:docs heroku-postgresql` to view documentation.

Promote the database (replace HEROKU_POSTGRESQL_INSTANCE with the name from the above output)

    $ heroku pg:promote HEROKU_POSTGRESQL_INSTANCE
      Ensuring an alternate alias for existing DATABASE... done, HEROKU_POSTGRESQL_COLOR
      Promoting HEROKU_POSTGRESQL_INSTANCE to DATABASE_URL on your-app-url... done

Create a new branch for any configuration/setup changes needed

    $ git checkout -b production

Deploy to Heroku

    $ git push heroku production:master
      Counting objects: 7, done.
      Delta compression using up to 4 threads.
      Compressing objects: 100% (3/3), done.
      Writing objects: 100% (4/4), 369 bytes | 0 bytes/s, done.
      Total 4 (delta 2), reused 0 (delta 0)
      remote: Compressing source files... done.
      remote: Building source:
      remote:
      remote: -----> Deleting 0 files matching .slugignore patterns.
      remote: -----> Using set buildpack heroku/php
      remote: -----> PHP app detected
      remote:
      remote:  !     WARNING: No 'composer.json' found.
      remote:        Using 'index.php' to declare app type as PHP is considered legacy
      remote:        functionality and may lead to unexpected behavior.
      remote:
      remote: -----> Bootstrapping...
      remote: -----> Installing platform packages...
      remote:        NOTICE: No runtime required in composer.lock; using PHP ^5.5.17
      remote:        - nginx (1.8.1)
      remote:        - php (5.6.20)
      remote:        - apache (2.4.20)
      remote: -----> Installing dependencies...
      remote:        Composer version 1.0.0 2016-04-05 13:27:25
      remote: -----> Preparing runtime environment...
      remote:        NOTICE: No Procfile, using 'web: vendor/bin/heroku-php-apache2'.
      remote: -----> Checking for additional extensions to install...
      remote:
      remote: -----> Discovering process types
      remote:        Procfile declares types -> web
      remote:
      remote: -----> Compressing...
      remote:        Done: 19.2M
      remote: -----> Launching...
      remote:        Released v1
      remote:        https://your-app-url.herokuapp.com/ deployed to Heroku
      remote:
      remote: Verifying deploy... done.
      To https://git.heroku.com/your-app-url.git
         875b112..79186a6  production -> master

After deployment WordPress has a few more steps to setup and thats it!

## Usage

Because a file cannot be written to Heroku's file system, updating and installing plugins or themes should be done locally and then pushed to Heroku.

## Updating

Updating your WordPress version is just a matter of merging the updates into
the branch created from the installation.

    $ git pull # Get the latest

Using the same branch name from our installation:

    $ git checkout production
    $ git merge master # Merge latest
    $ git push heroku production:master


