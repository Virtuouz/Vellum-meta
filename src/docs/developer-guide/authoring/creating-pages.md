---
_schema: default
draft: false
title: Creating Pages 
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: creating pages
  order: 
  title: Creating Pages
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

All pages need to be created in the `src/docs` folder. You will notice that some pages already exist see [File Structure Explained](src/docs/developer-guide/file-structure.md#docs) to learn about these pages.

## Creating a New Page
To create a new page all you have to do is create a new markdown file in the `src/docs` folder. For example, `src/docs/quick-start.md`.

### Adding front matter
Front matter is a way to add metadata to a page. It is a YAML block that starts with `---` and ends with `---`. You can copy and paste the front matter from another page to use as a starting point, or you can copy it from `.cloudcannon/schemas/doc.md`.

||| warning
**Important**

Front matter must start on line 1 of the file.
|||


::: tabs#front-matter
@tab:active Example front matter#example-front-matter
This is the front matter of this page for example:
+++ Front matter of this page
```md
---
_schema: default
draft: false
title: Creating Pages 
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: creating pages
  order: 
  title: Creating Pages
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
+++

@tab Default front matter#default-front-matter
Here is the blank front matter for a new page:
+++ Blank front matter, copy and paste this
```md
---
_schema: default
draft: false
title: Page
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: page
  order: 
  title:
  parent:
  url:
  icon:
pageLink: 
metaDesc: 
socialImage:
customCode:
  headCode: ""
  bodyCode: ""
tags:
editorial_blocks: []
---
```
+++

:::


## Front Matter Explained

### `_schema`
The `_schema` field is the name of the schema that will be used to validate the front matter. The default schema is `default`. You can find the schemas in the `.cloudcannon/schemas` folder, there is only one schema at this time.

This field is primarily for use within the Cloudcannon cms. If you aren't using Cloudcannon, you can safely ignore this field.

### `draft`
This a `true` or `false` field that indicates if the page is a draft. If it is a draft, the page will not be published. This is useful for pages that are not ready to be published yet.

### `title`
The `title` field is the title of the page. This is what will be displayed in the navigation bar.

### `eleventyExcludeFromCollections`
This a `true` or `false` field that indicates if the page should be excluded from the collections. A page marked as draft will have this value set to `true` at build time. This will prevent the page from showing up in 11ty collections which effectively means that it will not show up in any navigation or the sitemap.

### `eleventyNavigation`
This is the navigation for the page. It is an object that contains the following fields:

- `key`: The key of the navigation item. This is used to identify the navigation item in the navigation bar. If no title is provided, the key will be used as the title.
- `order`: The order of the navigation item. This is used to sort the navigation items.
- `title`: The title of the navigation item. This is what will be displayed in the navigation bar.
- `parent`: The parent of the navigation item. This is used to group the navigation items. What is placed in this field is the `eleventyNavigation.key` of the parent navigation item.
- `url`: This is if you want to link out to external pages, or to download files. If a value is set, the page will not build. This could also be used to link to internal pages.
- `icon`: The icon of the navigation item. This is used to display an icon next to the navigation item. All you have to do is type in the name of the icon. You can find the options here [heroicons.com](https://heroicons.com/). An example of of an icon name is `archive-box-arrow-down`

### `pageLink`
This is what the ending url of the page should be. For example a pagelink of `quick-start` would be `https://vellumdocs.dev/quick-start`. If this field is not set, the `title` field will be used as the `pageLink` instead. 

Whether a pagelink or the title is used, the value will be sluggified. This means that spaces will be replaced with hyphens and special characters will be removed. For example, a title of `Quick Start` will be `quick-start`. If you try do something like `/authoring/newpage/`, the slug will be `authoring-newpage`.

The only time a special character is allowed is a single `/`. This marks that page as the home page of a folder. Folder names become part of a pages url. To learn more read the routing documentation

### `metaDesc`
The `metaDesc` is the meta description of the page. This is used primarily for SEO purposes, but it can be left blank.

### `socialImage`
The `socialImage` is the image that will be used for social media sharing. This is used primarily for SEO purposes, but it can be left blank. A default social image can be setup in the `site.json` file.

### `customCode`
The `customCode` field is an object that contains two fields:

- `headCode`: The code that will be injected into the `<head>` of the page.
- `bodyCode`: The code that will be injected into the `<body>` of the page.

This functionality exists primarily for use within the Cloudcannon cms. Since you have direct code access you can add in your custom scripts where needed. That being said, this field can still be used to inject per page scripts.

### `tags`
The `tags` field is where you tag a page with a collection that you want it to be a part of. Even though this filed supports an array of tags, only 1 tag is recommneded. This field expects a `collection.key` which you can set up in the docCollections.json file.

### `editorial_blocks`
This is how users of cloudcannon CMS would create pages. Instead of markdown, they would be be using bookshop components that are part of the editorial_blocks structure. This can be ignored if you aren't using cloudcannon cms.

## Content Section
Everything past the front matter, the last `---` is the content of the page. This is where you would write your documentation in markdown. To see every every default markdown element, custom components, and how to write the markdown for them, check out the [styling page](src/docs/Styling.md).

Here is an example of this page:

+++ Meta Example
```md
---
_schema: default
draft: false
title: Creating Pages 
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: creating pages
  order: 
  title: Creating Pages
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

All pages need to be created in the `src/docs` folder. You will notice that some pages already exist see [File Structure Explained](src/docs/developer-guide/file-structure.md#docs) to learn about these pages.

## Creating a New Page
To create a new page all you have to do is create a new markdown file in the `src/docs` folder. For example, `src/docs/quick-start.md`.

### Adding front matter
Front matter is a way to add metadata to a page. It is a YAML block that starts with `---` and ends with `---`. You can copy and paste the front matter from another page to use as a starting point, or you can copy it from `.cloudcannon/schemas/doc.md`.
```
+++

