<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Custom-UI",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Custom UI"
}
-->

# Custom UI

Build your own reader screens on the SDK’s core: your archive, your reader screen, and the features you choose to add.

## Overview

A custom UI uses the core SDK directly. You fetch the catalog, open an
edition, and host [`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController), the page renderer the
prebuilt UI uses, inside a reader screen you design. It works with every
edition on PageSuite’s current system, classic PDF editions included: the
pages render exactly as they do in the prebuilt reader, and everything
around them is yours. “Feed” in API names such as
[`FeedEditionService`](/documentation/PSReader/FeedEditionService) is the current system’s old name, not a format.
Editions on the legacy replica system open only in the prebuilt UI; see
[Edition Platforms](/documentation/PSReader/Edition-Platforms).

```swift
// Your archive: here, the publication's newest edition.
let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
let published = try await service.latestEdition(
    publicationGUID: "PUBLICATION_GUID",
    publicationName: "The Daily"
)

// Your reader screen, which hosts the SDK's reader.
let screen = ReaderScreenViewController(published: published)
let navigationController = UINavigationController(rootViewController: screen)
navigationController.modalPresentationStyle = .fullScreen
present(navigationController, animated: true)
```

`ReaderScreenViewController` is the reader screen that
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader) builds, and every guide below adds to it.

![The sample's custom reader showing a classic PDF page with the app's own title, page label, and bookmark and download buttons.](images/com.pagesuite.PSReader/sample-custom-reader~dark@2x.png)

## Building Your Reader

A custom reader comes together in the same order as the sample app’s
Custom target, which [Build Your Own Reader Screen](/documentation/PSReader/Building-a-Reader-App#Build-Your-Own-Reader-Screen)
walks through:

1. **Fetch the catalog.** List a publication’s editions, or one month of
   them, with ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService``, and draw them in your own archive
   screen. See <doc://com.pagesuite.PSReader/documentation/PSReader/Fetching-the-Archive>.
1. **Open an edition.** Turn the edition the user picked into an edition
   source, with progress for your loading screen. See
   <doc://com.pagesuite.PSReader/documentation/PSReader/Opening-an-Edition>.
1. **Host the reader.** Present your reader screen, which embeds
   ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController``, follows the page on screen, and
   chooses single or double pages. See <doc://com.pagesuite.PSReader/documentation/PSReader/Hosting-the-Reader>.
1. **Build the chrome.** A page label, a page browser, and the settings
   your app offers, driven by the reader’s state. See
   <doc://com.pagesuite.PSReader/documentation/PSReader/Hosting-the-Reader#Building-the-Chrome> and
   <doc://com.pagesuite.PSReader/documentation/PSReader/Building-a-Page-Browser>.
1. **Add features.** A download button and a bookmark button first, then
   whatever else your app needs, each from the parts the SDK provides. See
   the tables below.

Common tasks, and where the guides cover them:

- **Open an edition from a link or notification:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Opening-an-Edition#Routing-Links-and-Notifications>
- **Open the latest edition from a button:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Fetching-the-Archive#Load-the-Catalog>
- **Resume where the user left off:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Opening-an-Edition#Resuming-Where-the-User-Left-Off>
- **Let users browse an archive by month:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Fetching-the-Archive#Listing-One-Month>
- **Label pages and spreads in your chrome:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Hosting-the-Reader#Labeling-Spreads>

[The Edition Model](/documentation/PSReader/The-Edition-Model) explains the models you’ll handle, and
[Identifiers](/documentation/PSReader/Identifiers) where each GUID comes from. Moving from the legacy core
SDK? Start with [Migrating From the Legacy Core SDK](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK).

## What You Build

The reader renders pages and reports what’s on screen. Everything the
prebuilt reader adds around the pages, you build, and the SDK supplies
what it can for each part.

Your reader screen:

|Part                       |You build                                                         |The SDK provides                                                                                                                                                                                                                                                                                                                  |Guide                                                                                                    |
|---------------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
|Archive                    |Your edition list                                                 |``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService``, by publication or by month                                                                                                                                                                                                                            |<doc://com.pagesuite.PSReader/documentation/PSReader/Fetching-the-Archive>                               |
|Loading screen             |Progress, the cover, and the edition’s name or date while it opens|Opening progress, and the cover, name, and date on ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished``                                                                                                                                                                                                           |<doc://com.pagesuite.PSReader/documentation/PSReader/Opening-an-Edition#Driving-a-Loading-UI>            |
|Edition dates              |Formatting each edition’s date for your archive and loading screen|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/editionDate``, falling back to ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/datePublished``. When ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/useCustomEditionName`` is `true`, show the edition’s `name` instead.|<doc://com.pagesuite.PSReader/documentation/PSReader/Fetching-the-Archive#Draw-the-Covers>               |
|Errors and offline         |Your error and offline states                                     |Typed errors, a cached catalog offline, and ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionErrorView`` for pages that fail                                                                                                                                                                                        |<doc://com.pagesuite.PSReader/documentation/PSReader/Fetching-the-Archive#Handle-Errors-and-Offline-Use> |
|Navigation bar and settings|All of it                                                         |The reader’s position, layout, and text size                                                                                                                                                                                                                                                                                      |<doc://com.pagesuite.PSReader/documentation/PSReader/Hosting-the-Reader#Building-the-Chrome>             |
|Double-page spreads        |When to show facing pages, in your layout delegate                |Spreads that pair a classic PDF edition’s pages as printed. Responsive editions show one page at a time. Without a layout delegate, the reader stays single-page.                                                                                                                                                                 |<doc://com.pagesuite.PSReader/documentation/PSReader/Hosting-the-Reader#Choosing-Single-or-Double-Pages> |
|Page browser               |A thumbnail overview                                              |Sections, page thumbnails, and friendly page labels                                                                                                                                                                                                                                                                               |<doc://com.pagesuite.PSReader/documentation/PSReader/Building-a-Page-Browser>                            |
|Dark mode                  |Your chrome’s colors                                              |Article and section pages, and the built-in advert pages, follow your screen’s light or dark appearance and re-render when it changes. PDF pages show as printed.                                                                                                                                                                 |                                                                                                         |
|Accessibility              |Labels for your chrome, and a text-size control                   |Article and section pages are web content, which VoiceOver reads. Their text size is ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEArticleTextSize``; they don’t follow Dynamic Type. The reader adds no accessibility information to PDF pages.                                                                       |<doc://com.pagesuite.PSReader/documentation/PSReader/Hosting-the-Reader#Article-Text-Size>               |
|Resuming                   |Saving the last page                                              |The settled page, and an opening page when you reopen                                                                                                                                                                                                                                                                             |<doc://com.pagesuite.PSReader/documentation/PSReader/Opening-an-Edition#Resuming-Where-the-User-Left-Off>|
|Deep links                 |Routing your URLs and notifications                               |Edition lookup by GUID                                                                                                                                                                                                                                                                                                            |<doc://com.pagesuite.PSReader/documentation/PSReader/Opening-an-Edition#Routing-Links-and-Notifications> |

Features:

|Feature               |You build                                                     |The SDK provides                                                                                                                                                             |Guide                                                                                                  |
|----------------------|--------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
|Downloads             |A download button and list                                    |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager`` and its observer                                                                                  |<doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Download-Button>                         |
|Download retention    |Removing old downloads, if your app does                      |Nothing expires downloads: they stay until removed, or until iOS clears the app’s caches when storage runs low. Each download records when it was queued.                    |<doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Download-Button#Managing-Stored-Editions>|
|Download while reading|Downloading an edition as the user opens it, if they choose to|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/downloadImmediately(published:)``, and an edition you can open as soon as its first pages are stored|<doc://com.pagesuite.PSReader/documentation/PSReader/Opening-an-Edition#Opening-While-Downloading>     |
|Bookmarks             |A bookmark button and list                                    |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager`` and its observer                                                                                  |<doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Bookmark-Button>                         |
|Sharing               |A share button                                                |``doc://com.pagesuite.PSReader/documentation/PSReader/ShareProvider`` and its link providers, unchanged                                                                      |<doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Share-Button>                            |
|Printing              |A print action                                                |Nothing yet                                                                                                                                                                  |<doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Share-Button#Printing>                   |
|Search                |A search screen                                               |``doc://com.pagesuite.PSReader/documentation/PSReader/FeedSearchService``                                                                                                    |<doc://com.pagesuite.PSReader/documentation/PSReader/Building-a-Search-Screen>                         |
|Text-to-speech        |A listen button                                               |``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechProvider``, overlay included                                                                        |<doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Listen-Button>                           |
|Commenting            |Forwarding the reader’s commenting delegate                   |``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider``                                                                                            |<doc://com.pagesuite.PSReader/documentation/PSReader/Adding-Comment-Buttons>                           |
|Adverts               |Any banners                                                   |Advert pages render built in, and the reader’s advert delegate can replace them                                                                                              |<doc://com.pagesuite.PSReader/documentation/PSReader/Handling-Advert-Pages>                            |
|Media and links       |Your gallery, player, and web view, and opening tapped links  |The reader’s media delegate, and a notification for each link it leaves to you                                                                                               |<doc://com.pagesuite.PSReader/documentation/PSReader/Handling-Media-and-Link-Taps>                     |
|Paywalls              |All of it: check entitlement before each open and download    |Nothing                                                                                                                                                                      |<doc://com.pagesuite.PSReader/documentation/PSReader/Gating-Editions-Behind-a-Paywall>                 |
|Analytics             |Most of it                                                    |The reader’s delegates, as the source of your events; ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel`` still reports downloads and bookmarks             |<doc://com.pagesuite.PSReader/documentation/PSReader/Reporting-Analytics>                              |

You can also mix in prebuilt screens. Open an edition from your own
archive in the prebuilt reader with [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController), or keep
the carousel and build only one screen yourself; see
[Mixing Prebuilt and Custom UI](/documentation/PSReader/Choosing-an-Integration#Mixing-Prebuilt-and-Custom-UI).

## Topics

### Your Reader

[Fetching the Archive](/documentation/PSReader/Fetching-the-Archive)

Load a publication’s editions and draw your own archive screen.

[Opening an Edition](/documentation/PSReader/Opening-an-Edition)

Turn a catalog entry into an edition source that your reader screen can show.

[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader)

Build your own reader screen around the SDK’s edition reader: the screen
every custom-UI guide adds to.

[Building a Page Browser](/documentation/PSReader/Building-a-Page-Browser)

Give users a thumbnail overview of the edition in your own reader screen,
and jump the reader to the page they tap.

### Adding Features

[Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button)

Add a download button to your own reader screen or archive that stores editions for offline reading, and list what’s on the device, with the SDK’s download manager.

[Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button)

Add a bookmark button to your own reader screen that saves the page or article in view, then list and reopen what the user saved.

[Adding a Share Button](/documentation/PSReader/Adding-a-Share-Button)

Add a share button to your own reader screen that shares the page in view, using the share providers the prebuilt reader uses.

[Building a Search Screen](/documentation/PSReader/Building-a-Search-Screen)

Build your own search screen that searches your publications’ editions with the SDK’s search service and opens results in your own reader screen.

[Adding a Listen Button](/documentation/PSReader/Adding-a-Listen-Button)

Add a listen button to your own reader screen that reads the article in view aloud, with the SDK’s text-to-speech provider.

[Adding Comment Buttons](/documentation/PSReader/Adding-Comment-Buttons)

Show comment buttons and counts on the articles in your own reader screen, with the SDK’s commenting provider.

[Handling Advert Pages](/documentation/PSReader/Handling-Advert-Pages)

Let the reader in your own reader screen render advert pages, or serve them from your own ad stack, and place any banners in your chrome.

[Handling Media and Link Taps](/documentation/PSReader/Handling-Media-and-Link-Taps)

Respond to taps on the images, videos, embeds, hotspots, and links in the pages your own reader screen hosts.

[Gating Editions Behind a Paywall](/documentation/PSReader/Gating-Editions-Behind-a-Paywall)

Check the user’s entitlement before your own screens open or download an edition, and show your paywall when they need one.

[Reporting Analytics](/documentation/PSReader/Reporting-Analytics)

Report what the user opens, views, saves, and shares in your own screens to your analytics provider.

