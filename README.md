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

`ey recipes download-custom <recipe1> <recipe2>` will download `custom-recipe` and `custom-recipe2` into `cookbooks`, and append the necessary `depends` lines to `cookbooks/ey-custom/recipes/after-main.rb`.
