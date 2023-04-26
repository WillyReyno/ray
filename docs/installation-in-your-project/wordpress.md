---
title: WordPress
weight: 4
---

There are several ways to install Ray in WordPress.

## Global installation

The easiest ways is the global installation. This will make the `ray()` function available in any WordPress (and PHP file on your system).

Issue these commands to install [the global-ray package](https://github.com/spatie/global-ray):

```bash
composer global require spatie/global-ray
global-ray install
```

You can now use the `ray()` function and all of its [framework agnostic capabilities](https://spatie.be/docs/ray/v1/usage/framework-agnostic-php). In each WordPress app you can also use these functions:

- `dump($variable)`: dump any kind of variable to the CLI.
- `dd($variable)`: dump any kind of variable to the CLI and terminate the script.

To use [the WordPress specific capabilities of Ray](https://spatie.be/docs/ray/v1/usage/wordpress), you should install `wordpress-ray` into the WordPress app.

## Manually cloning the repo

Inside the `wp-content/plugins` directory run this command

```bash
git clone git@github.com:spatie/wordpress-ray
```

## Installing Ray via the WordPress admin UI

Ray is also registered as [a plugin on WordPress.org](https://wordpress.org/plugins/spatie-ray/). In the admin section of WordPress, go to "Plugins" > "Add New", and search for "Spatie Ray".

![screenshot](/docs/ray/v1/images/wp-install.png)

Install and activate the plugin.

## Must use Plugins

By default WordPress loads your plugins in the following order:
- Checks for any must-use plugins directory (default = /wp-content/mu-plugins).
- Then, if you're running a multisite installation, it checks for plugins that are network-activated and loads those.
- Then it checks for all other active plugins by looking at the active_plugins entry of the wp_options database table, and loops through those. The plugins will be listed alphabetically.

If you wish to debug your plugins within the Ray app it is recommended that you install the plugin into your `/wp-content/mu-plugins` directory. Further details on Must Use Plugins can be [found here](https://wordpress.org/support/article/must-use-plugins/):

To install, inside the `wp-content/mu-plugins` directory run this command:

```bash
git clone git@github.com:spatie/wordpress-ray
```

Next, from the just created `wordpress-ray` directory, run this command:

```bash
composer install -o --no-dev
```

You'll then need to create `ray-loader.php` within `/wp-content/mu-plugins` and include the following code:

```php
require WPMU_PLUGIN_DIR.'/wordpress-ray/wp-ray.php';
```

## Setting Environment variable

When developing locally you should have `WP_ENVIRONMENT_TYPE` set as `local` in your `wp-config.php` otherwise Ray won't work.

```php
define( 'WP_ENVIRONMENT_TYPE', 'local' );
```

