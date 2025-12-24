---
_schema: default
draft: false
title: Creating Change Logs 
eleventyExcludeFromCollections: false
date:
eleventyNavigation:
  key: Creating Change Logs
  order: 
  title: Creating Change Logs
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
Vellum has a built-in change log feature that can be used to track changes to your documentation, or anything else that you like to track in a change log style format. Additionally a RSS feed is provided for change logs which also sanitizes the components to an RSS compliant format.

This changelog supports and correctly renders components created using markdown or bookshop components when used in CloudCannon.

An example of the changelog in use in this site can be found [here](src/docs/changelog.md).

## Setup
The only thing necessary to start using the change log feature is to flag documents as change logs. To do this, add the `changeLog` tag to the front matter of the document. You don't even have to define the a `changelog` doc collection. However, it is required to define a doc collection with a `changelog` key if change logs will be created using CloudCannon. The change log will render the 10 most recent change logs when pagination is not used.

```diff-md
---
  _schema: default
  draft: false
  title: Added Change Log
  eleventyExcludeFromCollections: false
  date: 2025-12-24T14:00:00-07:00
  eleventyNavigation:
    key: Added Change Log
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
+ tags: changelog
  editorial_blocks: []
---
```

### Adding Pagination
If you want to add pagination to your change logs, you can add a `pagination` object to the front matter of the page that will be used as the primary change log page. Pagination is not required, but is likely desired.


```diff-md
---
  _schema: default
  draft: false
  title: Changelog
  eleventyExcludeFromCollections: false
  eleventyNavigation:
    key: Changelog
    order: 100
    title:
    parent:
    url:
    icon: clipboard-document-list
  pageLink: /changelog/
+ pagination:
+   data: collections.changelog
+   size: 10
+   reverse: true
+   generatePageOnEmptyData: true
  metaDesc: 
  socialImage:
  customCode:
    headCode: ""
    bodyCode: ""
  tags: vellum
  editorial_blocks: []
---
```
The flag of `generatePageOnEmptyData` is not required, but if not set, the page will not render if there are no change logs. We set `reverse: true` so that the most recent change logs are at the top of the page.

After pagination has been set the changelog component will handle rendering the next and previous links.

You can learn more about 11ty pagination [here](https://www.11ty.dev/docs/pagination/){target=_blank}.

## Using the Change Log
After there are some existing change logs created, you can then add in the changelog bookshop component into the content body of the document and it'll render the change log.

||| warning
**Note**

Slashes added to prevent liquid from being interpreted. Don't use slashes to actually render the change log.
|||
```liquid
\{\% bookshop 'simple/changelog' \%\}
```

## Pro Tips
### Organizing Change Logs
It is recommended to place your change logs in a separate folder from the other documentation. This will make it easier to find and manage them. If expect to generate many change logs, a fil structure such as `src/docs/changelogs/<year>/<month>/<yyyy-mm-dd>-<title>.md` might be useful. 11ty can infer the date from a files name if following the format of `yyyy-mm-dd-<title>.md`. This means that setting the date in the front matter is not required.

### `eleventyNavigation`
For change logs, the `eleventyNavigation` front matter key can be mostly ignored as the `changelog` collection is prevent from showing up in the collection selector. The sidebar navigation also wont render for change log pages.

