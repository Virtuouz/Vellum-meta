---
_schema: default
draft: false
title: Quick Start
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: Quick Start 
  order: 0
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
Getting started with Vellum and writing content can happen in just a few minutes.

## 1. Copy the starter template
The first thing you'll need to do is make a copy of the Vellum template. It will come minimally setup so you can start writing your content right away.

Create a by clicking on `Use this template`

https://github.com/Virtuouz/vellum

## 2. Clone the repo locally
Once you have created your copy of the template, you can clone the repo locally.

## 3. Install and intial setup
After cloning run the following commands

1. `npm run install`
2. `npm run build` (this will create indexing for search and generate the sites favicon) <br> Newly created pages will not be indexed and you'll need to run `npm run build` again
3. `npm run start` (this will start the dev server)

You should be able to see the site at `http://localhost:8080`

## That's it!
You can now start writing your documentation in the `src/docs` folder. 

To learn how to create new pages, check out the [creating pages guide](src/docs/developer-guide/authoring/creating-pages.md).

## Next Steps
1. Configure your sites theme. See [site-wide configuration](src/docs/developer-guide/site-wide.md)
2. Read through the File Structure guide to learn more about all the files that make up the site. [File Structure Explained](src/docs/developer-guide/file-structure.md)