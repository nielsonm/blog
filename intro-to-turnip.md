## What is Turnip?
[Turnip](https://github.com/opensourcery/turnip) is a Drupal starter kit created by the OpenSourcery as starting point on scratch built Drupal installs.  Turnip provides a basic setup that puts site builders several steps ahead of the vanilla Drupal install.

Furthermore,  Turnip adds a host of community contributed modules that make up the core sitebuilding & development functionality at the OpenSourcery. This post is the first of a series highlighting the tools & methodologies that make up Turnip.

## What are the components?

The main components of Turnip are:

*  Drush make
*  Profiler
*  Features
*  Behat
*  Deploy

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

Profiler is a neat library that extends the functionality of the install profile.  Gone are the days where custom install profiles meant long and largely unreadable database updates.  Followed by obscure Drupal function calls and more database queries.
With profiler, creating basic placeholder content is done in a human readable format.  Even custom fields can be included given the proper set of parameters.
It all starts out with the install profile's .info file.  Adding a placeholder node is as simple as this.

```
nodes[about][type] = page
nodes[about][title] = About
nodes[about][body][und][0][value] = PLACEHOLDER
nodes[about][body][und][0][format] = full_html
nodes[about][uid] = 1
nodes[about][language] = und

```

The above example isn't exactly easy, but it is quite a bit more straightforward than creating a node object and calling `node_save()`.

### Features
Features is a way to assemble and export site components into a custom module.  Features can be exported via the interface in the site itself.  The feature can then be tracked in source control, making transferring settings from dev to test site and then onto deployment more straightforward.
#### Module development, point & click style
Features shine at taking things that are built in the UI like permissions or views. The components are then exported to a custom includes file specific to the components in the feature. Features can be managed via drush using commandes like `features-update` or `features-revert` to move features out of the database into code or the reverse.
### Behat
Behat is a framework, independent of Drupal that tests whether or not software behaves in a given way. Since the software is being tested on a more interface driven level, the tests can be less specific to verifying the state of a variable.  The upshot of Behat it is that the tests are designed to be human readable and writable.

#### Testing on the client side

Since tests can be almost directly ported from user stories, the responsibility of writing the tests can be reassigned from the developer or the QA lead to a Project Manager or possibly even the client.  Tests can be tagged to differentiate levels of depth, or even browser versions.

### Deploy
Deploy is a project that uses the Universally Unique Identifier (UUID) to export staged content, much in the same way that Features indentifies and exports site architecture, deploy exports and manages content.

NEW BLOG POST

## How do I install Turnip?
Definitely refer to the Turnip README [available here.](https://github.com/opensourcery/turnip) for extended directions on the step-by-step.

### Verifying drush
Since building the drupal site proper depends on drush, it's vital to make sure that drush is installed.  To verify that, simply type `drush --version` into your terminal.  If it returns version 5 or above, you're good to go.

Once you've verified drush, we're going to skip to the action packed step (# 3), where we actually start building the site.  Run `bin/make-install-profile` with the arguments directed in the README.  This script will only need to be run once as the turnip default profile name will be set using this name.  The git tip to use `git add -A` should be a must-use.  Completing this step means that the profile is now stubbed out and ready to run install.

Now that the profile build has been started, this is when things get interesting.  Run `bin/install` to get the ball rolling and install the make file,  building the actual drupal site.  It will start scrolling down, showing all the modules being downloaded into the profile. Once the build finishes, the drupal install is located in `/drupal`. The install profile is located in the `/profiles` directory which in turn has a `/modules` directory where all the modules are installed.
