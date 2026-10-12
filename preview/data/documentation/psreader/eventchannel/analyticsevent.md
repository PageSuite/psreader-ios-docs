<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O"
  },
  "title" : "EventChannel.AnalyticsEvent"
}
-->

# EventChannel.AnalyticsEvent

An analytics event and any relevant context associated with the event.

```
enum AnalyticsEvent
```

## Overview

Events named `feedEdition…` come from editions on PageSuite’s current
system, classic PDF or responsive, and events named `replica…` from
legacy replica editions. [Edition Platforms](/documentation/PSReader/Edition-Platforms) explains the names.

## Topics

### Carousel Navigation

[`EventChannel.AnalyticsEvent.carouselView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/carouselView(_:))

Fires when a carousel page is viewed.

### Opening Editions

[`EventChannel.AnalyticsEvent.feedEditionLaunch(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionLaunch(_:))

Fires when an edition is launched from the archive.

### Page Views

[`EventChannel.AnalyticsEvent.feedEditionSectionView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionSectionView(_:))

Fires when a section front is viewed.

[`EventChannel.AnalyticsEvent.feedEditionArticleView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionArticleView(_:))

Fires when an article is viewed.

[`EventChannel.AnalyticsEvent.feedEditionReplicaView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionReplicaView(_:))

Fires when a classic PDF page is viewed.

[`EventChannel.AnalyticsEvent.feedEditionOtherPageView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionOtherPageView(_:))

Fires when a page is viewed that is not otherwise
covered by a view event.

[`EventChannel.AnalyticsEvent.feedEditionBookmarkView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionBookmarkView(_:))

Fires when a bookmarked article is viewed.

### Downloads

[`EventChannel.AnalyticsEvent.feedEditionDownloaded(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionDownloaded(_:))

Fires when an edition is downloaded.

[`EventChannel.AnalyticsEvent.feedEditionDeleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionDeleted(_:))

Fires when an edition download is deleted.

### Bookmarks

[`EventChannel.AnalyticsEvent.feedEditionArticleBookmark(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionArticleBookmark(_:))

Fires when an article is bookmarked.

[`EventChannel.AnalyticsEvent.feedEditionArticleBookmarkDeleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionArticleBookmarkDeleted(_:))

Fires when an article bookmark is deleted.

[`EventChannel.AnalyticsEvent.feedEditionPageBookmark(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionPageBookmark(_:))

Fires when a page is bookmarked.

[`EventChannel.AnalyticsEvent.feedEditionPageBookmarkDeleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionPageBookmarkDeleted(_:))

Fires when a page bookmark is deleted.

### Sharing

[`EventChannel.AnalyticsEvent.feedEditionShare(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionShare(_:))

Fires when a page is shared.

[`EventChannel.AnalyticsEvent.feedEditionShareBookmark(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionShareBookmark(_:))

Fires when a bookmarked article is shared.

### Search

[`EventChannel.AnalyticsEvent.searchCompleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/searchCompleted(_:))

Fires when a search query completes and results are returned.

[`EventChannel.AnalyticsEvent.searchResultTapped(_:_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/searchResultTapped(_:_:))

Fires when a user taps a search result.

### Replica Editions

[`EventChannel.AnalyticsEvent.replicaLaunch(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaLaunch(_:))

Fires when a replica edition is launched from the archive.

[`EventChannel.AnalyticsEvent.replicaPageView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageView(_:))

Fires when a replica page is viewed.

[`EventChannel.AnalyticsEvent.replicaArticleView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleView(_:))

Fires when a replica popover article is viewed.

[`EventChannel.AnalyticsEvent.replicaArticleTapped(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleTapped(_:))

Fires when a replica popover article is tapped.

[`EventChannel.AnalyticsEvent.replicaDownloaded(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaDownloaded(_:))

Fires when a replica edition is downloaded.

[`EventChannel.AnalyticsEvent.replicaDeleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaDeleted(_:))

Fires when a replica edition download is deleted.

[`EventChannel.AnalyticsEvent.replicaPageBookmark(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageBookmark(_:))

Fires when a replica page is bookmarked.

[`EventChannel.AnalyticsEvent.replicaPageBookmarkDeleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageBookmarkDeleted(_:))

Fires when a replica page bookmark is deleted.

[`EventChannel.AnalyticsEvent.replicaArticleBookmark(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleBookmark(_:))

Fires when a replica popover article is bookmarked.

[`EventChannel.AnalyticsEvent.replicaArticleBookmarkDeleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleBookmarkDeleted(_:))

Fires when a replica popover article bookmark is deleted.

[`EventChannel.AnalyticsEvent.replicaPageShare(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageShare(_:))

Fires when a replica page is shared.

[`EventChannel.AnalyticsEvent.replicaArticlePageShare(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticlePageShare(_:))

Fires when a replica popover article is shared.

[`EventChannel.AnalyticsEvent.replicaPagePrint(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPagePrint(_:))

Fires when a replica page is printed.

[`EventChannel.AnalyticsEvent.replicaArticlePagePrint(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticlePagePrint(_:))

Fires when a replica popover article is printed.

[`EventChannel.AnalyticsEvent.replicaPageLinkTapped(_:_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageLinkTapped(_:_:))

Fires when a URL is tapped in a replica page view.

[`EventChannel.AnalyticsEvent.replicaArticleLinkTapped(_:_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleLinkTapped(_:_:))

Fires when a URL is tapped in a replica article view.

[`EventChannel.AnalyticsEvent.replicaArticleTextSizeChange(_:oldValue:newValue:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleTextSizeChange(_:oldValue:newValue:))

Fires when replica popover article text size preference is changed.

[`EventChannel.AnalyticsEvent.replicaPageBrowserOpen(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageBrowserOpen(_:))

Fires when the replica page browser is opened.

[`EventChannel.AnalyticsEvent.replicaPageBrowserSectionTapped(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageBrowserSectionTapped(_:))

Fires when the user taps a section in the replica page browser.

[`EventChannel.AnalyticsEvent.replicaPageBrowserNextTapped(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageBrowserNextTapped(_:))

Fires when the user taps the Next button in the replica page browser / bottom navigation bar.

[`EventChannel.AnalyticsEvent.replicaPageBrowserPreviousTapped(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageBrowserPreviousTapped(_:))

Fires when the user taps the Previous button in the replica page browser / bottom navigation bar.

[`EventChannel.AnalyticsEvent.replicaArticleBrowserOpen(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleBrowserOpen(_:))

Fires when the user opens the replica article browser.

[`EventChannel.AnalyticsEvent.replicaArticleBrowserSectionTapped(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleBrowserSectionTapped(_:))

Fires when the user taps a section in the replica article browser.

[`EventChannel.AnalyticsEvent.replicaArticleBrowserNextTapped(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleBrowserNextTapped(_:))

Fires when the user taps the Next button in the replica article browser / bottom navigation bar.

[`EventChannel.AnalyticsEvent.replicaArticleBrowserPreviousTapped(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleBrowserPreviousTapped(_:))

Fires when the user taps the Previous button in the replica article browser / bottom navigation bar.

