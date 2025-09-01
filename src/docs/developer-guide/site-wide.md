---
_schema: default
draft: false
title: Site-Wide Configuration 
eleventyExcludeFromCollections: false
eleventyNavigation:
  key: Site-Wide Configuration
  order: 100
  title: null
  parent: setup
  url: null
  icon:
pageLink: 
metaDesc: null
socialImage: null
customCode:
  headCode: ''
  bodyCode: ''
tags: dev
editorial_blocks: []
---
The information in this section is more technical, but it should still make sense if you are using the visual editor

Vellum's global settings are managed through a few key files located in the `src/_data/` directory. These files allow you to control everything from your site's name and logo to its color scheme and announcement banner.

||| warning
**Note** 

You will see an `_inputs` key in many of the files below. This is is used to define the inputs within the Cloudcannon cms. You are not using Cloudcannon, you can safely ignore this key. 
|||


## Theme (`theme.json`)
This file controls the entire visual appearance of your site.

- **Colors:** The `light` and `dark` objects contain the color palettes for the two display modes. You can change any of these values to match your brand's aesthetic.
- **Fonts:** You can change the typography of your site by updating the `heading_font`, `content_font`, and `logo_font` values. Simply enter the name of any font available on [Google Fonts](https://fonts.google.com/ "null"), and Vellum will handle the rest. For example this site is using `{{theme.heading_font}}` for the headings and `{{theme.content_font}}` for the body text.

### Setting Up Theme Colors
Below is a breakdown of how each color variable is used throughout the site:
- `background-body`: The main background color for the entire page.
- `background-surface`: Used for elements layered on top of the body, such as sidebars, dropdowns, and accordion backgrounds.
- `background-interactive-hover`: The background color for interactive elements when a user hovers over them, like links in the navigation sidebar.
- `text-primary`: The primary text color used for headings and body paragraphs.
- `text-muted`: The color for secondary or less emphasized text, such as strikethroughs in tasklists.
- `border-primary`: The color for primary borders and horizontal rules (`<hr>`).
- `accent-primary`: The main brand color used for links, active tabs, and other highlighted elements.
- `accent-hover`: The color of primary accent elements when hovered.
- `accent-secondary`: A secondary brand color for additional highlights.
- `accent-secondary-hover`: The hover state for the secondary accent color.
- `code-inline-background`: The background for `code` snippets that appear within a line of text.
- `code-inline-text`: The text color for inline `code` snippets.
- `code-block-background`: The background for larger, multi-line code blocks (`<pre>`).


### Setting up Fonts
Any of the fonts from Google Fonts can be used for headings, body text, and logo text. All you have to do is type in name of the font, includign capitals and spacing.

For example if you want to use Alegreya Sans SC you would type `Alegreya Sans SC`

    

## Site Details (`site.json`)

This file contains general information about your website.

- **name:** The name of your website, used in the browser tab and metadata.
- **url:** The full URL of your live website (e.g., `https://example.com`).
- **logoLightPath & logoDarkPath:** The paths to your logo for light and dark modes, respectively.
- **faviconPath:** The path to your site's favicon.
- **socialImage:** An image that will be shown when your site is shared on social media.
- **customCode:** Allows advanced users to inject code (like analytics scripts) into the `<head>` or `<body>` of every page.
    

## Announcement Banner (`banner.yml`)

This file controls the site-wide notification banner that appears at the top of the page.

- **enable_banner:** A simple switch to turn the banner on (`true`) or off (`false`).
- **markdown:** The content of the banner. You can use Markdown here for formatting like **bold** or _italics_.
- **id:** A unique identifier for the banner. This helps the site remember if a user has closed it. If you want the banner to reappear for everyone, simply change this ID.
- **show_until:** The banner will automatically hide itself after this date and time.
- **backgroundColor & textColor:** The colors used for the banner's background and text.
    

## Document Collections (`docCollections.json`)

This file defines the different documentation "Collections" for your site. Each collection in the list is an object with the following properties:

- **key:** A short, unique identifier for the collection (e.g., "vellum").
- **name:** The full, user-friendly name that appears in the dropdown menu (e.g., "Vellum").
- **icon:** The name of the icon to display next to the collection name. Vellum uses Heroicons; you can find a list of names on their website.
- **path:** The URL that the collection links to when selected.