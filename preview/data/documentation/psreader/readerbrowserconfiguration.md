<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderBrowserConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader26ReaderBrowserConfigurationV"
  },
  "title" : "ReaderBrowserConfiguration"
}
-->

# ReaderBrowserConfiguration

Configuration object used to customize the appearance of the reader content browser.

```
struct ReaderBrowserConfiguration
```

## Overview

The content browser allows users to navigate sections, pages, and articles within an edition.

Customize this configuration to control the colors, typography, and visual highlights of sections,
pages, and articles, aligning with your app’s overall style and user experience requirements.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Theming>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/ReaderBrowserConfiguration/init(globalConfig:))

Initializes a new content browser configuration using the provided global SDK configuration.

### Appearance

[`backgroundColor`](/documentation/PSReader/ReaderBrowserConfiguration/backgroundColor)

Background color of the content browser view.

[`liquidGlassPolicy`](/documentation/PSReader/ReaderBrowserConfiguration/liquidGlassPolicy)

Liquid Glass policy for the reader content browser.

[`assetDelegate`](/documentation/PSReader/ReaderBrowserConfiguration/assetDelegate)

Delegate used for placeholder images.

### Sections

[`sectionBackgroundColor`](/documentation/PSReader/ReaderBrowserConfiguration/sectionBackgroundColor)

Background color of unselected section items in the browser.
Defaults to `dynamicSectionColor` meaning every section has it’s own section color.

[`currentSectionBackgroundColor`](/documentation/PSReader/ReaderBrowserConfiguration/currentSectionBackgroundColor)

Background color of the currently selected section item. Use an alpha less than 1
to have the `sectionBackgroundColor` bleed through.

[`dynamicSectionColor`](/documentation/PSReader/ReaderBrowserConfiguration/dynamicSectionColor)

Sentinel value indicating we should use section specific colors.

[`sectionLabel`](/documentation/PSReader/ReaderBrowserConfiguration/sectionLabel)

Appearance configuration for unselected section labels.

[`currentSectionLabel`](/documentation/PSReader/ReaderBrowserConfiguration/currentSectionLabel)

Appearance configuration for the currently selected section label.

[`sectionDividerEnabled`](/documentation/PSReader/ReaderBrowserConfiguration/sectionDividerEnabled)

Indicates whether visual dividers are displayed between section items.

### Pages and Articles

[`pageTitleLabel`](/documentation/PSReader/ReaderBrowserConfiguration/pageTitleLabel)

Appearance configuration for unselected page titles.

[`currentPageTitleLabel`](/documentation/PSReader/ReaderBrowserConfiguration/currentPageTitleLabel)

Appearance configuration for the currently selected page title.

[`articleTitleLabel`](/documentation/PSReader/ReaderBrowserConfiguration/articleTitleLabel)

Appearance configuration for unselected article titles.

[`currentArticleTitleLabel`](/documentation/PSReader/ReaderBrowserConfiguration/currentArticleTitleLabel)

Appearance configuration for the currently selected article title.

[`pageInfoLabel`](/documentation/PSReader/ReaderBrowserConfiguration/pageInfoLabel)

Appearance configuration for labels showing page information (e.g., page numbers).

[`currentlyReadingLabel`](/documentation/PSReader/ReaderBrowserConfiguration/currentlyReadingLabel)

Appearance configuration for the “currently reading” indicator label.

### Pages and Articles Toggle

[`toggleTitleLabel`](/documentation/PSReader/ReaderBrowserConfiguration/toggleTitleLabel)

Appearance configuration for content toggle button titles in their default (unselected) state.

[`selectedToggleTitleLabel`](/documentation/PSReader/ReaderBrowserConfiguration/selectedToggleTitleLabel)

Appearance configuration for content toggle button titles when selected.

[`toggleBackgroundColor`](/documentation/PSReader/ReaderBrowserConfiguration/toggleBackgroundColor)

Background color for content toggle buttons in their unselected state.

[`selectedToggleBackgroundColor`](/documentation/PSReader/ReaderBrowserConfiguration/selectedToggleBackgroundColor)

Background color for the selected content toggle button.

