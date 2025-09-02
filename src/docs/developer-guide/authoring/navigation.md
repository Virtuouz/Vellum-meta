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

||| error
**Work in progress**

This page is a work in progress.
|||

Creating and writing content in pages is half of what makes a documentation site. The other half is the navigation. Vellum uses the `eleventy-navigation` plugin to create the navigation for you, this removes alot of the manual work with creating navigation links, but it does require some learning.

Pretty much all navigation on this website for this template is determined by the documentation pages themselves. There isn't a global navigation file where everything has to be set up.

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

## Sidebar Navigation
The sidebar navigation is generated automatically from all the document based internal linking through the `eleventy-navigation` plugin.

||| warning
**Common Mistake**

Its a common mistake to finish setting up the eleventyNavigation of a page and then to forget to add it to a collection by adding the collection key to the pages `tags` field. A page without a collectio association will never show up in the sidebar navigation.
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

### Parent Pages Shouldn't have Content
