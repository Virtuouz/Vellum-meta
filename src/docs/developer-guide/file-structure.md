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


## File structure refernce

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


