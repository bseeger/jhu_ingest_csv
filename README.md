# JHU Sample Migration for testing

## Introduction

This repository is based on the work done in the [islandora/migrate_islandora_csv](https://github.com/islandora/migrate_islandora_csv) repository.

This repository, __jhu_ingest_csv__, is a test repository to help migrate some sample JHU data into Drupal 8 using Migrate tools to create Islandora content in 8.  It can be used as a template for ingests.  You might find it helpful as another example to follow when working with migrations.  The test data includes Image, Audio and PDF files. 

This repository contains a `data` folder containing a CSV and the sample files, as a convenience so that the accompanying files are easily available on the Drupal server running the migration. (This is not the recommended method for making files available to Drupal in a real migration.)

This repository may function as a template for JHU (and others) to create the yml files defining migrations.

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

Optionally, flush the cache (`drush cr`), so the migrations become visible in the GUI at Manage > Structure > Migrations > jhu_ingest_csv (http://localhost:8000/admin/structure/migrate/manage/jhu_ingest_csv/migrations)

Now lets go migrate some files.

Cautionary sidenote: as you saw, you can still `git clone` into the modules directory, but if you're installing a custom module that's intended to stay installed for the long term (unlike a migration feature, which you should probably uninstall and delete when you're done with it) then you may want to check with your devops folks and use Composer instead. However, using Git directly allows you to be more flexible when iterating and testing.

## Configuration

No configuration page is provided.

This module uses Features, which is an easy way to ship and install Drupal configuration. To make changes, edit the configuration files in this module and use Features to import those changes. There is a walkthrough in the "Configuration" section of the [Migrate 7.x to 8](https://github.com/Islandora-Devops/migrate_7x_claw) tutorial. 

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
