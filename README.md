# JHU Sample Migration for testing

## Introduction

This repository is based on the work done in the [islandora/migrate_islandora_csv](https://github.com/islandora/migrate_islandora_csv) repository.

This repository, __jhu_ingest_csv__, is a test repository to help migrate some sample JHU data into Drupal 8 using Migrate tools to create Islandora content in 8.  It can be used as a template for ingests.  You might find it helpful as another example to follow when working with migrations.  The test data includes Image, Audio and PDF objects.

This repository contains a `data` folder containing a CSV and the sample files, as a convenience so that the accompanying files are easily available on the Drupal server running the migration. (This is not the recommended method for making files available to Drupal in a real migration.)

This repository may function as a template for JHU (and others) to create the yml files defining migrations.

There are three sample imports in this repository: 
- one containing collections 
- one containing digital resources with one image or pdf
- one containing more complex resources - paged content (this one also contains a few one image resources as well)

There is also a template CSV file. 

## Requirements

This module requires the following modules:

* [islandora/islandora_defaults](https://github.com/Islandora/islandora_defaults)
* This repository (jhu_ingest_csv)

## Installation

From your `islandora-playbook` directory, issue the following commands to enable this module:
- `vagrant ssh` to open a shell in your Islandora instance.
- `cd /var/www/html/drupal/web/modules/contrib` to get to your modules directory.
- `git clone https://github.com/bseeger/jhu_ingest_csv` to clone down the repository from GitHub.
- `drush en -y jhu_ingest_csv` to enable the module, installing the migrations as configuration.

_Note: you need to change the Rights field to work with larger rights statement. There is a 255 character limit that needs to be changed to 1500 for these ingests (or you can trim the data in the CSV files).  To change the limit in the drupal UI:  Structure->ContentType->Repository Object->Manage Fields-> edit the Rights field._

Optionally, flush the cache (`drush cr`), so the migrations become visible in the GUI at Manage > Structure > Migrations > jhu_ingest_csv (http://localhost:8000/admin/structure/migrate/manage/jhu_ingest_csv/migrations)

Now you're ready to migrate some files.  For a tutorial on how to do that, please visit: 
[migrate_islandora_csv/TUTORIAL.md](https://github.com/Islandora/migrate_islandora_csv/blob/dev/TUTORIAL.md).  For basic instructions, please read on. 

Cautionary sidenote: as you saw, you can still `git clone` into the modules directory, but if you're installing a custom module that's intended to stay installed for the long term (unlike a migration feature, which you should probably uninstall and delete when you're done with it) then you may want to check with your devops folks and use Composer instead. However, using Git directly allows you to be more flexible when iterating and testing.

### Install instructions

This will just give the commands for how to run the migration.  For a more in-depth tutorial on how to do that and what is going on at each step, please visit: [migrate_islandora_csv/TUTORIAL.md](https://github.com/Islandora/migrate_islandora_csv/blob/dev/TUTORIAL.md).  For basic instructions, please read on. 

The key to the ingest is to ingest items in this order: 
* files
* nodes
* media

If you don’t ingest the files and nodes first, media ingest will fail as Media are the items that associate a Node with a File. 

First, if not already on the server:

`vagrant ssh`

Then, we need to be in drupal web space:

`cd /var/www/html/drupal/web/modules/contrib/jhu_ingest_csv`  

(see above about how to enable the module, if you already haven't)

#### Collections

First, ingest collections: 

`drush -y --userid=1 --uri=localhost:8000 migrate:import collections`

Now you will have few nodes that are collections in your system. The example includes showing how to create a subcollection.

#### Files, Nodes, Media

This next section will show how to import the first set of data - simple one image or one pdf resources. 

First, start with the files: 

`drush -y --userid=1 --uri=localhost:8000 migrate:import file_1`

(Note: From here on out you can use the Islandora UI (Structure -> Migrations, jhu_ingest_csv -> List migrations). (_Note: In theory,
you can use the UI from the start, but I haven't seen that be the case until after the files are in._)

Or you can continue on command line: 

`drush -y --userid=1 --uri=localhost:8000 migrate:import node_1`

`drush -y --userid=1 --uri=localhost:8000 migrate:import media_1`

From here the system will spend a bit of time doing all the behind the scenes things after the ingest is complete: making derivatives, running FITS on the files.   Objects will not look complete in the UI because of this.  After an install, give it a little space to do it’s work and you should see complete objects (with thumbnails, etc) shortly. 

## Configuration

No configuration page is provided.  Note that changes to configuration files will not be read in by the system.  The file will need to be reloaded. To learn how to do this, read on.

This module uses the Features Module, which is an easy way to ship and install Drupal configuration. To make changes to a configuration, edit the configuration files in this module and use Features to import those changes. There is a walkthrough in the "Configuration" section of the [Migrate 7.x to 8](https://github.com/Islandora-Devops/migrate_7x_claw) tutorial. 

## Documentation

Further documentation about migrations is available on the [Islandora 8 documentation site](https://islandora.github.io/documentation/).

## Troubleshooting/Issues

Having problems with migrations or solved a problem? Check out the Islandora google groups for a solution.

* [Islandora Group](https://groups.google.com/forum/?hl=en&fromgroups#!forum/islandora)
* [Islandora Dev Group](https://groups.google.com/forum/?hl=en&fromgroups#!forum/islandora-dev)

## Maintainers/Sponsors

Current maintainers:

* [Bethany Seeger](https://github.com/bseeger)

## License

[GPLv2](./LICENSE).
