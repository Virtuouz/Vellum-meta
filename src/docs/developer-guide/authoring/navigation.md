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

## Document Collections
The `docCollections.json` file is as "global" as the navigation will get, everything else will be set up in the individual pages' frontmatter.

This file creatse your "cabinets" for your documentation site. All documentation must be associated to a collection. If you only create a single collection, and assign all documents to that collection, your website will work more like traditional documentation sites and the option to switch between collections will be hidden.

> If you only create a single collection, and assign all documents to that collection, your website will work like more traditional documentation sites and the option to switch between collections will be hidden.

## Internal linking
It's a common use case to link out to other pages from within a page. However, knowing what the url of the page is can be tricky since Vellum creates permalinks dynamically. Even when you explcitly set a `pageLink` for a page, Vellum will still take into account all of the pages parent folders and make them part of the final url.

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

The a `path` for each collection can also use a relative path, which will also automatically update when the url of the page changes.

Here is there `docCollections.json` file of this site:
```json
{{docCollections | json: 4}}
```


