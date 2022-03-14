# Opigno Drupal Distribution for Platform.sh

<p align="center">
<a href="https://console.platform.sh/projects/create-project?template=https://raw.githubusercontent.com/platformsh/template-builder/master/templates/drupal8-opigno/.platform.template.yaml&utm_content=drupal8-opigno&utm_source=github&utm_medium=button&utm_campaign=deploy_on_platform">
    <img src="https://platform.sh/images/deploy/lg-blue.svg" alt="Deploy on Platform.sh" width="180px" />
</a>
</p>

This template builds the Opigno Drupal 8 distribution using the [Drupal Composer project](https://github.com/drupal-composer/drupal-project) for better flexibility.  It also includes configuration to use Redis for caching, although that must be enabled post-install in `.platform.app.yaml`.

Opigno is a Learning Management system built as a Drupal distribution.

## Features

* PHP 7.3
* MariaDB 10.4
* Redis 6
* Drush and Drupal Console included
* Automatic TLS certificates
* Composer-based build

## Post-install

Run through the Opigno installer as normal.  You will not be asked for database credentials as those are already provided.

## Customizations

The following changes have been made relative to Drupal 8 / Opigno as it is downloaded from Drupal.org.  If using this project as a reference for your own existing project, replicate the changes below to your project.

* It uses the Drupal Composer project, which allow the site to be managed entirely with Composer. That also causes the `vendor` and `config` directories to be placed outside of the web root for added security.  See the [Drupal documentation](https://www.drupal.org/node/2404989) for tips on how best to leverage Composer with Drupal 8.
* The `.platform.app.yaml`, `.platform/services.yaml`, and `.platform/routes.yaml` files have been added.  These provide Platform.sh-specific configuration and are present in all projects on Platform.sh.  You may customize them as you see fit.
* An additional Composer library, [`platformsh/config-reader`](https://github.com/platformsh/config-reader-php), has been added.  It provides convenience wrappers for accessing the Platform.sh environment variables.
* A `.environment` file has been added, which allows executable app dependencies from Composer to be run from the path.
* Drush and Drupal Console have been pre-included in `composer.json`.  You are free to remove one or both if you do not wish to use them.  (Note that the default cron and deploy hooks make use of Drush commands, however.)
* The Drupal Redis module comes pre-installed.  The placeholder module is not pre-installed, but it is enabled via `settings.platformsh.php` out of the box.
* The `settings.platformsh.php` file contains Platform.sh-specific code to map environment variables into Drupal configuration. You can add to it as needed. See the documentation for more examples of common snippets to include here.  It uses the Config Reader library.
* The `settings.php` file has been heavily customized to only define those values needed for both Platform.sh and local development.  It calls out to `settings.platformsh.php` if available.  You can add additional values as documented in `default.settings.php` as desired.  It is also setup such that when you install Drupal on Platform.sh the installer will not ask for database credentials as they will already be defined.

## References

* [Drupal](https://www.drupal.org/)
* [Opigno](https://www.opigno.org)
* [Drupal on Platform.sh](https://docs.platform.sh/frameworks/drupal8.html)
* [PHP on Platform.sh](https://docs.platform.sh/languages/php.html)
