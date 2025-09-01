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


