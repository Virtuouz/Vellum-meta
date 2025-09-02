---
_schema: default
draft: false
title: Navigation (Page Routing)
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: navigation
  order: 
  title: Navigation (Page Routing)
  parent: authoring
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
{% assign demoTitle = title | slugify %}

Creating and writing content in pages is half of what makes a documentation site. The other half is the navigation. Vellum uses the `eleventy-navigation` plugin to create the navigation for you, this removes alot of the manual work with creating navigation links, but it does require some learning.

Pretty much all navigation on this website for this template is determined by the documentation pages themselves. There isn't a global navigation file where everything has to be set up.

## How Vellum Generates permalinks (Page Urls)
You'll notice that the frontmatter for each page has a `pageLink` key. This is the url that will be used for the page. If no pagelink is set, the `title` of the page will be used as the url.

It is commonly desired to have more meaningful URLs such as `example.com/help/getting-started`. If you try to create a page with a pagelink of `help/getting-started`, it will be convereted into `help-getting-started` which is not what you wanted.

To achieve this you would instead need to create a `help` folder in which the `getting-started` page would be created. See the example below.

```ultree
. (Vellum root)
  src
    docs
      help
        getting-started.md
```

Even though 11ty supports explicity definition of permalinks for each page, Vellum creates permalinks dynamically based on the pages relative path, `pagelink` and page `title` when `pageLink` is not set.

The only time a special character is allowed is a single `/`. This marks that page as the home page of a folder. If used at the top level `docs` folder, then that page will become home page of the site.

### Manually Setting Permalinks
If you want to manually set the permalink for a page, you can do so by adding the `permalink` key to the frontmatter. The `permalink` key is the url that will be used for the page.

To learn more about permalinks checkout this [11ty documentation](https://www.11ty.dev/docs/permalinks/)

If permalink exists in the frontmatter of a page, the dynamica permalinking will be ignored.

```diff-md
---
  _schema: default
  draft: false
  title: Navigation (Page Routing)
  eleventyExcludeFromCollections: false
  eleventyNavigation:
    key: navigation
    order: 
    title: Navigation (Page Routing)
    parent: authoring
    url:
    icon:
  pageLink:
+ permalink: "help/getting-started/index.html" 
  metaDesc: 
  socialImage:
  customCode:
    headCode: ""
    bodyCode: ""
  tags: dev
  editorial_blocks: []
---
```

## Handling Duplicate Permalinks
11ty be default fails to build if there are duplicate permalinks. This is great behavior for a dev, but confusing for a non-technical user who is using Vellum within Cloudcannon.

During development of Vellum a decision was made that duplicate permalinks would not cause a build to fail, and instead would append a `-copy-1` to the end of the duplicate permalinks where `1` is how many times that page has been duplicated. This decision was made because Vellum creates permalinks dynamically and is thus at a higher risk of creating duplicate permalinks.

If you are working with Cloudcannon CMS, it is recommended to keep this behavior for your users. If you aren't working with Cloudcannon CMS, you can keep this functionality or disable if you'd rather your site fail to build if there are duplicate permalinks (default 11ty behavior).

### Catching Duplicate Permalinks
If you are keeping the duplicate permalinks behavior, then you'll need to be on the look out for when a duplicate permalink has been created.

Since this duplicate check happens at build time, it can easily happen when developing locally and it can be missed. The duplicate permalink check script works by adding a `permalink` key to the frontmatter of a page if a duplicate permalink is found, this prevents future duplicates, but it means that page will forever have a `-copy-1` at the end of the permalin if not caught. The best way to see if a page has had this key added is check which files have been updated through `git status`. 

||| info
**Avoiding headaches**

To avoid headaches, it is recommended to disable the duplicate permalink behavior if you won't be working with Cloudcannon CMS, and plan to work on the project locally.
|||

### Disable Duplicate Permalink Check
To disable the duplicate permalink check, you'll need to first:

1. Find and open the eleventy.config.js file
2. Locate `eleventyConfig.on("eleventy.before", ()` which as towards the end of the file
3. Either remove or comment out `execSync("node ./utils/permalinkDupCheck.js");`




## Internal linking
**This is an important topic**, so it'll be explained first. It's a common use case to link out to other pages from within a page. However, knowing what the url of the page is can be tricky since Vellum creates permalinks dynamically. Even when you explcitly set a `pageLink` for a page, Vellum will still take into account all of the pages parent folders and make them part of the final url.

Instead of manually deciphering what the url of a page would be, you can instead just use the pages relative path instead. 

For example instead of knowing that the url of this page will be:

{{permalink | renderContent | replace: 'undefined', demoTitle | replace: 'index.html', ''}}

You can instead use the pages relative path:

`src/docs/developer-guide/authoring/navigation.md`

Now if the url of this page ever changes, it'll automatically update anywhere this relative path is referenced as a link. 

+++ Example linking to another page
This is me linking to another page: [here](src/docs/developer-guide/authoring/creating-pages.md)

```md
This is me linking to another page: [here](src/docs/developer-guide/authoring/creating-pages.md)
```
+++

Using a pages relative path works anywhere a link can be created. In more technical terms, if it becomes part of an `href` attribute, 11ty will replace the relative path with the correct url.

The `path` for each collection can also use a relative path, which will also automatically update when the url of the page changes.

### Collections reference example
Here is there `docCollections.json` file of this site:
```json
{{docCollections | json: 4}}
```

## Document Collections
The `docCollections.json` file is as "global" as the navigation will get, everything else will be set up in the individual pages' frontmatter.

This file creatse your "cabinets" for your documentation site. All documentation must be associated to a collection. If you only create a single collection, and assign all documents to that collection, your website will work more like traditional documentation sites and the option to switch between collections will be hidden.

> If you only create a single collection, and assign all documents to that collection, your website will work like more traditional documentation sites and the option to switch between collections will be hidden.

Even though documents are associated to a collection, the collection name does not become part of the URL.

The `path` key of a collection is the url of a page that is to act as the home page for that collection. [See the example above as a reference.](#collections-reference-example)

### Adding a Page to a Collection
To add a page to a collection, you must a set a pages `tags` field to that collections `key`.

In the this example below, this page is part of the `dev` collection, so it will show up in the sidebar navigation for that collection.

+++ Example adding a page to a collection
```diff-md
---
  _schema: default
  draft: false
  title: Navigation (Page Routing)
  eleventyExcludeFromCollections: false
  eleventyNavigation:
    key: navigation
    order: 
    title: Navigation (Page Routing)
    parent: authoring
    url:
    icon:
  pageLink: 
  metaDesc: 
  socialImage:
  customCode:
    headCode: ""
    bodyCode: ""
+ tags: dev
  editorial_blocks: []
---
```
+++

## Sidebar Navigation
The sidebar navigation is generated automatically from all the document based internal linking through the `eleventy-navigation` plugin.

||| warning
**Common Mistake**

Its a common mistake to finish setting up the eleventyNavigation of a page and then to forget to add it to a collection by adding the collection key to the pages `tags` field. A page without a collection association will never show up in the sidebar navigation.
|||

### `eleventyNavigation`
It is an object that contains the following fields:

- `key`: The key of the navigation item. This is used to identify the navigation item in the navigation bar. If no title is provided, the key will be used as the title.
- `order`: The order of the navigation item. This is used to sort the navigation items.
- `title`: The title of the navigation item. This is what will be displayed in the navigation bar.
- `parent`: The parent of the navigation item. This is used to group the navigation items. What is placed in this field is the `eleventyNavigation.key` of the parent navigation item.
- `url`: This is if you want to link out to external pages, or to download files. If a value is set, the page will not build. This could also be used to link to internal pages.
- `icon`: The icon of the navigation item. This is used to display an icon next to the navigation item. All you have to do is type in the name of the icon. You can find the options here [heroicons.com](https://heroicons.com/). An example of of an icon name is `archive-box-arrow-down`

Below is the frontmatter for this page:

```md
---
_schema: default
draft: false
title: Navigation (Page Routing)
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: navigation
  order: 
  title: Navigation (Page Routing)
  parent: authoring
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
```

Notice how in the `eleventyNavigation` field, the parent is set to `authoring`. This means that this page will show up in the sidebar navigation under the `Authoring` section.

Here is the front matter for the "Authoring" page:
```md
---
_schema: default
draft: false
title: Authoring
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: authoring
  order: 100
  title: Authoring
  parent: null
  url: null
  icon: null
pageLink: null
metaDesc: null
socialImage: null
customCode:
  headCode: ''
  bodyCode: ''
tags: dev
editorial_blocks: []
---
```

This page is stating that the authoring page is its parent.

||| error 
**Parent Pages Shouldn't have Content**

If page is going to be used as a parent page to nest other pages under it, then it shouldn't have any content. Parent pages are still generated, but they aren't navigable to in the sidebar. This choice was made to streamline the functionality of dropdowns so that they are easy to use for users.
|||