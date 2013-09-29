## What is Turnip?
Turnip is a Drupal starter kit created by the OpenSourcery as starting point on scratch built Drupal installs.  Turnip provides a basic setup that puts site builders several steps ahead of the vanilla Drupal install.

Furthermore,  Turnip adds a host of community contributed modules that make up the core sitebuilding & development functionality at the OpenSourcery. This post is the first of a series highlighting the tools & methodologies that make up Turnip.

## What are the components?

The main components of Turnip are:

*  Drush make
*  Profiler
*  Features
*  Behat
*  Migrate

Individually they represent codebase, installation, configuration management, testing and content staging tools.  Together they allow devs to build complex websites that can be deployed and built on nearly any platform with little adaptation.

### Drush make

Drush make is a sub-command of Drush (If you haven't of Drush, stop right now and go check it out, it *will* change the way you develop with Drupal forever.)
Drush make is a package manager (like `composer`, `apt-get`, or `gem`) that can, given a manifest of modules, download them to a central location ready for use.

These manifests, or lists of modules are composed into make files.  Drupal doesn't interface with these directly, which is why you need Drush installed.

Unlike the old days of Drupal, where a distrobution contained not only the custom code created by the maintainers, but Drupal core and all the contrib modules the custom code depended upon.  Drush make files can track the core and contrib versions and download them.  All that is needed is a path to put the contrib modules.

```

projects[drupal][type] = "core"
projects[drupal][version] = "7.23"
projects[mollom][version] = "2.7"

```

Since the OpenSourcery uses install profiles, we prefer to put any and all contrib modules in `/profiles/PROJECT_NAME/modules/contrib`.
Custom modules can be put into `custom` and any features in `features` (more on features later).

Furthermore Drush make is even more useful given when modules aren't exactly perfect in their stable release state.  Given enough time working on Drupal projects and one is bound to find a bug in a module.
One of the greatest things about Open Source Software, and doubly so for Drupal, is that bugs are discussed publicly and the fixes are available immediately.  Bugs are first fixed using files called patches.  Oftentimes patches exist for a module long before the maintainers see fit to roll a new release.  If the fix exists, but isn't part of the code base yet, what's a dev to do?  Patching the module and entering it into source control is one option, but any and all changes to the module in the future must also be tracked for the duration of the project.
Luckily enough, drush make allows projects to have patches applied to a given project.  This is an even bigger win, if you discover a bug in a contrib module, figure out the fix for it, and submit the patch to fix it on Drupal.org!  You get a working module, street cred for posting a patch, and the community gets a more stable, workable product.  EVERYONE WINS!

To build the site, simply run `drush make PATH/TO/MAKEFILE DRUPAL_DIRECTORY`.  If you forget the exact command to build the site in drush, no worries. Just use `bin/rebuild` and the site will be built in the `/drupal` directory.

### Profiler

Profiler is a neat library that extends the functionality of the install profile.  Gone are the 

### Features
### Behat
### Deploy

## How do I install it?
### Verifying drush
### Verifying behat
