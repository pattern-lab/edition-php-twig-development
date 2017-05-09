# Pattern Lab Development Edition for Twig

> THIS IS A FORK! All deps points to forks on [Drupal Pattern Lab](https://github.com/drupal-pattern-lab) org.

The Development Edition for Twig allows the core team to work on and commit changes to the latest editions of select Twig-related components while running each one within the overall Pattern Lab environment. This edition is **NOT** stable.

Drupal Pattern Lab fork at [Pattern Lab Standard Edition for Twig](https://github.com/drupal-pattern-lab/edition-php-twig-standard) is the stable version. Please start there for all your Twig needs.

## Packaged Components

The Development Edition for Twig installs the **`dev` branch** from each of the following components, all forks:

* `pattern-lab/core`: [GitHub](https://github.com/drupal-pattern-lab/patternlab-php-core)
* `pattern-lab/patternengine-twig`: [GitHub](https://github.com/drupal-pattern-lab/patternengine-php-twig)
* `pattern-lab/starterkit-twig-demo`: [GitHub](https://github.com/drupal-pattern-lab/starterkit-twig-demo)
* `pattern-lab/styleguidekit-assets-default`: [GitHub](https://github.com/drupal-pattern-lab/styleguidekit-assets-default)
* `pattern-lab/styleguidekit-twig-default`: [GitHub](https://github.com/drupal-pattern-lab/styleguidekit-twig-default)
* `pattern-lab/unified-asset-installer`: [GitHub](https://github.com/drupal-pattern-lab/unified-asset-installer)

## Installing the Development Edition for Twig

Pattern Lab uses [Composer](https://getcomposer.org/) to manage project dependencies. If you are going to use the Development Edition you are required to have Composer installed.

### 1. Install Composer

Please follow the directions for [installing Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx) on the Composer website. We recommend you [install it globally](https://getcomposer.org/doc/00-intro.md#globally).

### 2. Install the Development Edition

After cloning this repo, `cd` into it and run:

    composer create-project

Now, all the dependencies above are in `vendor/pattern-lab` and are repos pointing to the above locations. You'll be able to work on forks of specific dependencies and see how it all works together this way.

### 3. Fix git remotes of dependencies

    composer run fix-git-remotes

See "Update Git Remotes" below for more info on why and what this does.

## Helpful Commands

These are some helpful commands you can use on the command line for working with Pattern Lab.

### List all of the available commands

To list all available commands type:

    php core/console --help

To list the options for a particular command type:

    php core/console --help --[command]

### Generate Pattern Lab

To generate the front-end for Pattern Lab type:

    php core/console --generate

### Watch for changes and re-generate Pattern Lab

To watch for changes and re-generate the front-end for Pattern Lab type:

    php core/console --watch

### Start a server to view Pattern Lab

You can use PHP's built-in web server to review your Pattern Lab project in a browser. In a seperate window type:

    php core/console --server

Then open [http://localhost:8080](http://localhost:8080) in your browser.

### Install a StarterKit

To install a near-empty StarterKit as a starting point for your project type:

    php core/console --starterkit --init

To install a specific StarterKit from GitHub type:

    php core/console --starterkit --install <starterkit-vendor/starterkit-name>

### Update Git Remotes

The command `composer run fix-git-remotes` will do this for you; but here's background that's good to know.

Due to an issue with Composer the default `remote` values for the `dev` branches are set to the wrong locations. This will cause issues if/when you try to push your changes. To update them you must type:

    git config branch.dev.remote origin

for each package. The list of packages included in the Development Edition and their locations are:

    pattern-lab/core -> vendor/pattern-lab/core/
    pattern-lab/unified-asset-installer -> vendor/pattern-lab/unified-asset-installer
    pattern-lab/patternengine-twig -> packages/pattern-lab/patternengine-twig
    pattern-lab/starterkit-twig-default -> packages/pattern-lab/starterkit-twig-default
    pattern-lab/styleguidekit-assets-default -> packages/pattern-lab/styleguidekit-assets-default
    pattern-lab/styleguidekit-twig-default -> packages/pattern-lab/styleguidekit-twig-default

**Important:** If you add another Pattern Lab package (e.g. plug-in, StarterKit, etc.) you must also make sure to update the origin for its `dev` branch.

## Adding a New Package

To add a new package to your version of the Development Edition for Twig type:

    composer require package-name/from-packagist

Composer uses [Packagist](http://packagist.com) as the repository of [all Pattern Lab-related packages](https://packagist.org/packages/pattern-lab/) from the core Pattern Lab team.

**Important:** If you add another Pattern Lab package (e.g. plug-in, StarterKit, etc.) you must also make sure to update the origin for its `dev` branch. [See instructions above](#update-git-remotes).

## Forking and Testing a Package

To use the Development Edition to test changes you may have made to a fork of a package do the following:

### 1. Fork a Package and Create a Feature Test Branch

On GitHub you can fork the package you want to modify. You must create a new branch in which you will create your new changes. In this example we will use `pattern-lab/patternengine-mustache` as the example of our forked project and `bugfix` as the name of our branch.

### 2. Update the Repositories Section of `composer.json`

In `composer.json` you need to add or update the `repositories` section to point at your forked repository for a package:

    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/your-name/patternengine-php-mustache"
        }
    ],

### 3. Update the Package Branch in Require Section of `composer.json`

In `composer.json` you need to update the `require` section to point at the new branch in your forked repository:

    "require": {
        "pattern-lab/patternengine-twig": "dev-bugfix"
    }

**Reminder:** `dev-` is used by Composer to know when it should clone a branch in a repo instead of downloading it. `dev-` should not he a part of the name of your branch.

### 4. Update the Development Edition's Dependencies

To update the Development Edition's dependencies to use your forked package type:

    composer update pattern-lab/patternengine-twig

## Testing Against "Releases"

Packages developed by the core Pattern Lab team use the [gitflow model](http://nvie.com/posts/a-successful-git-branching-model/) of Git repository management. Because the Development Edition clones the repos for each package you can technically switch each package to use the `master` branch to test against the last release of any particular package.
