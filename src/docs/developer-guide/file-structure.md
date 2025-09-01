---
_schema: default
draft: false
title: File Structure Explained
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: File Structure Explained
  order: 
  title:
  parent: setup
  url:
  icon:
pageLink: 
metaDesc: 
socialImage:
customCode:
  headCode: ""
  bodyCode: ""
tags: dev
editorial_blocks: []
---
The file structure of Vellum follows that of an 11ty project. Almost everything that is important lives in the `src` directory. 

## File structure reference

||| info
**Info**

You can collapse the root directory or any other directories of the file structure by clicking on the folder name.
|||

```ultree
. root
  _component-library
    (contents ommited)
  .cloudcannon
    schemas
      doc.md
  dist
    (output directory)
  src
    _data
    _includes
      layouts
        base.html
        doc.html
        page.html
      partials
        banner.html
        favicon.html
        google-fonts.html
        meta-info.html
        render-sidebar.html
    assets
      images
        uploads
      js
      styles
    docs
      404.md
      docs.11tydata.js
      docs.json
      home.md
      robots.njk
      sitemap.njk
    filters
      extract-file-substring-filter.js
      pathExists-filter.js
      uuid-filter.js
  utils
    build-theme.js
    generateFavicon.js
    permalinkDupCheck.js
  cloudcannon.config.yml
  eleventy.config.js
  tailwind.config.js
```



## `_component-library`
This is where all the bookshop components live. These components are primarily for the users who are using the visual editor within Cloudcannon. If you are planning to write documentation in markdown, you don't need to worry about these components.

### Extending the component library
If you are interested in expanding the component library, whether for your own use or your stakeholders, you would create those here. To create a new component you can use the following command:

`npm run new <component-name>`

Going into detail on component authoring is out of scope for this documentation, but you can explore the `_component-library` directory for examples.


Here are official guides from Cloudcannon as well on how to create new components:

* https://cloudcannon.com/documentation/guides/bookshop-eleventy-guide/component-templating/

## `.cloudcannon`
This is another Cloudcannon specific. This directory can be ignored for the most part as everything that needs to be setup here has been done already.

### `.cloudcannon/scehemas`
This is primarily for cloudcannon, but it can be useful for copying the contents of the `doc.md` file into a new file for creating new pages.

## `src` the important folder
`src` contains all the files that are necessary for the site to be built. You will also be writing your documentation in the subfolder(s) of `src/docs`.

### `_data`
In 11ty this is known as your global data. Any files created here can be accessed globally by the site and that makes this the best place to create config style files for the site. Global data files and its contents can be referenced from anywhere on the site.

For example this is the current heading font for the site: `{{theme.heading_font}}`

```liquid
\{\{theme.heading_font\}\}
```
||| info
**Note**

If `\` was removed it would just retrieve the font instead and thus they were added to escape the liquid.
|||

Going into all the details of how 11ty works is out of scope for this documentation. If you are interested in learning more about 11ty, check out the

* [11ty docs](https://www.11ty.dev/docs/).
* [11ty global data](https://www.11ty.dev/docs/data-global/)

Here is also an 11ty course that, while outdated in terms of the latest version of 11ty, is still a good resource to learn the fundamentals. If you try to follow the course step by step, it will fall apart on module 18 and I don't recommended continueing past that point.

https://learneleventyfromscratch.com/

### `_includes`
This is where you can create reusable includes. This template has a few layouts which can be found in the `src/_includes/layouts` directory. There are also some partials which can be found in the `src/_includes/partials` directory. The files here are what are used to build the site.

The structure of a page is built as follows:

```ultree
Completed Page
  base.html
    Referenced Partials
      meta-info.html
      banner.html
      favicon.html
      google-fonts.html
    doc.html (uses base.html)
      Referenced Partials
        render-sidebar.html
```

You can find more information about includes [here](https://www.11ty.dev/docs/layouts/). 

### `assets`
This is where all the assets for the site are stored. This includes images, js, and css.

#### `assets/images`
Here you will find all the icons available to be used by the site. These are just the heroicons from [heroicons.com](https://heroicons.com/)

`assets/images/uploads` this is where you can upload your own images to be used on the site. Feel free to create subfolders here.

#### `assets/js`
This is where all the js files are stored. There is currently only one file here and it is the `table-saw.js` file. This is responsible for creating responsive tables at small screen sizes.

Almost all other logic that runs this site can be found in the base.html layout file, or as [hyperscript](https://hyperscript.org/) code where needed. 

#### `assets/styles`
All styles are stored here. This includes global styles, component styles, and content styles.

### `docs`
This is where you'll likely live after initial site setup. You will be creating all of your documentation files within this folder. You are free to add in subfolders as you need to help you organize your documentation.

A simple system that can help you stay organized is to create a folder for each of your collections. You can also create subfolders for documentation that will be nested into dropdown menus.

#### `docs/404.md`
This is the page that is shown when a page is not found. Notice how it is just a page that has some markdown. You can choose to update the existing markdown to your liking. You can however create a dedicated layout for the 404 page that has more bells and whistles to suit your needs.

#### `docs/docs.11tydata.js`
This is a data file that computes data at run time. This file is what determines if a page should build or not based on the `draft` property.

This should be left alone.

#### `docs/docs.json`
This data file sets the default values for the `permalink` and `layout` attributes for each page. The default value for the permalink is actually liquid code that is used to create dynamic permalinks. Please refer to the routing documentation for more information

Generally this should be left alone.

#### `docs/robots.njk`
This is a file that is used to create the robots.txt file. Feel free to modify this file to your liking to suit your web crafting needs.

#### `docs/sitemap.njk`

This is a file that is used to create the sitemap.xml file. 

Generally this should be left alone.

### `filters`
This is where custom liquid filters have been created and where you can create your own filters.

* https://www.11ty.dev/docs/filters/
* https://www.11ty.dev/docs/languages/javascript/#filters

### `utils`
This is where utility functions that run during the build step have been created. This is where you will find the 

* `build-theme.js`
* `generateFavicon.js`
* `permalinkDupCheck.js` (more on this in the routing documentation) 

## `.cloudcannon.config.yml`
This is the global Cloudcannon configuration file. If you aren't planning to use the visual editor, you can ignore this file.

If you are using the visual editor, here is the documentation for the config file. This is using the new unified configuration for Cloudcannon.

https://cloudcannon.com/documentation/articles/what-is-the-cloudcannon-configuration-file/

## `eleventy.config.js`
This is the global eleventy configuration file. This is where custom filters, 11ty plugins, and other custom configurations can be added.

https://www.11ty.dev/docs/config/

## `tailwind.config.js`
This is the global tailwind configuration file. This is where custom tailwind configurations have been added to support the user defined theme.

