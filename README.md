# EY Cloud Recipes for V5

This is designed to be a starting point for your V5 custom chef repository. It is a perfectly valid, albeit empty, chef repository. You can run `ey recipes upload -e <your_environment_name>`, click Apply, and you will not get any errors. It does nothing, though. To get it to do something, you need to download recipes.

## Quick Start

Clone this repository

```
git clone git@github.com:radamanthus/ey-cloud-recipes-V5.git
```

Download some repositories

```
cd ey-cloud-recipes-V5
ey recipes download-custom redis resque
```

Upload

```
ey recipes upload -e my_environment_name
```

Click Apply on the dashboard to upload the recipes to  the instances and run them.

## Downloading recipes

Running `ey recipes download-custom <recipe1> <recipe2>` will do the following:

1. Download `custom-recipe` and `custom-recipe2` into `cookbooks`, and 
2. Append the lines below to `cookbooks/ey-custom/recipes/after-main.rb`:

```
depends 'custom-recipe'
depends 'custom-recipe2'
```

## What is the deal with the "recipe" and "custom-recipe" cookbooks?

While maintaining our custom cookbook repository we need to satisfy two conflicting goals:

1. Keep the recipes up-to-date with the latest packages and security fixes
2. Provide our customers flexibility in customizing the recipes

The [Cookbook Wrapper Pattern](https://blog.chef.io/2013/12/03/doing-wrapper-cookbooks-right/) allows us to support both goals. For example, for solr, the "solr" recipe is the core recipe. It installs downloads and installs the Solr search server. The "custom-solr" recipe is for customizing solr. We will try to provide as much customization hooks into the core recipes, so that you should be able to implement your customizations by only modifying the "custom-recipe" recipes.

<a name="migrating-from-v4"></a>
## Migrating V4 Custom Chef to V5

This might require changes to your custom recipes due to stack changes. You might need to update the full paths bundle (/usr/local/bin/bundle), rake (/usr/bin/rake), and other system gems, otherwise some recipes and deploy hooks can break.

If your recipe installs packages, update the package versions. To get the package versions on V5, ssh to an instance and run eix <package name>, i.e. ex dev-db/redis.

Here are the V5 versions for the commonly used packages:

| Package     | Gentoo Package Name   | Latest V5 Version | Default Installed Version |
| ---         | ---                   | ---:              | ---:                      |
| ImageMagick | media-gfx/imagemagick | 7.0.1.6           | 6.9.4.1                   |
| Java        | dev-java/icedtea-bin  | 3.0.1             | 3.0.1                     | 
| Redis       | dev-db/redis          | 3.2.0             | 2.8.23-r1                 |
| Sphinx      | app-misc/sphinx       | 2.2.10            | 2.1.9                     |
| TinyProxy   | net-proxy/tinyproxy   | 1.8.3-r4          | Not Installed             |
| Varnish     | www-servers/varnish   | 4.1.2             | Not Installed             |