<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Prebuilt-UI",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Prebuilt UI"
}
-->

# Prebuilt UI

A complete reader app you configure: edition archives, the reader, downloads, bookmarks, and search, styled to match your brand.

## Overview

The prebuilt UI is a finished reader experience. Show all of it from one
[`CarouselViewController`](/documentation/PSReader/CarouselViewController):

```swift
import PSReader
import UIKit

let globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE")
    ]
)
window.rootViewController = carousel
```

**iPhone:**

![The carousel showing a dynamic archive: the section ribbon, subsection pills, and a grid of edition covers.](images/com.pagesuite.PSReader/carousel-dynamic-archive~dark@2x.png)

**iPad:**

![The carousel showing a dynamic archive: the section ribbon, subsection pills, and a grid of edition covers.](images/com.pagesuite.PSReader/carousel-dynamic-archive-ipad~dark@2x.png)

The shortcode loads your publications, their archives, and their reader
settings from PageSuite. From there you configure rather than build:
fonts, colors, and icons come from your [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration), and
delegates connect your paywall, sharing, analytics, and other services.

The carousel’s screens also work one at a time, in an app with its own
navigation, and [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) opens any edition in the
prebuilt reader from a button or a link. Every screen takes the same
configuration and delegates as the carousel.

The prebuilt UI opens every edition on PageSuite’s current system,
classic PDF and responsive editions alike, and editions on the legacy
replica system too (see [Edition Platforms](/documentation/PSReader/Edition-Platforms)). To design every screen
yourself instead, see [Custom UI](/documentation/PSReader/Custom-UI).

## Building Your App

The guides below follow the order you’d build in:

1. **Set up.** Show the whole app with <doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>, or
   place its screens in your own navigation with
   <doc://com.pagesuite.PSReader/documentation/PSReader/Embedding-Prebuilt-Screens>. Either way, open editions from your
   own buttons, links, and notifications with
   <doc://com.pagesuite.PSReader/documentation/PSReader/Presenting-the-Prebuilt-Reader>.
1. **Theme.** Give every screen your fonts, brand color, and icons with
   <doc://com.pagesuite.PSReader/documentation/PSReader/Theming>. <doc://com.pagesuite.PSReader/documentation/PSReader/Configuring-the-Prebuilt-UI> explains how those
   values reach each screen, and how to change one screen on its own.
1. **Customize the reader.** Choose what the reader’s navigation bar,
   content browser, splash screen, and settings menu show with
   <doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>, and translate the interface with
   <doc://com.pagesuite.PSReader/documentation/PSReader/Localization>.
1. **Add features.** Start with <doc://com.pagesuite.PSReader/documentation/PSReader/Paywalls> if your editions are for
   subscribers, then add what your app needs: downloads, bookmarks,
   search, sharing, commenting, text-to-speech, adverts, media, and
   analytics. Each has its own guide under Features.

Common tasks, and where the guides cover them:

- **Open an edition from a link or notification:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Presenting-the-Prebuilt-Reader#Routing-Links-and-Notifications>
- **Open the latest edition from a button:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Presenting-the-Prebuilt-Reader#Choosing-an-Initializer>
- **List editions in a screen of your own:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Presenting-the-Prebuilt-Reader#Listing-Editions-Yourself>
- **Add a Continue Reading button:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Presenting-the-Prebuilt-Reader#Adding-a-Continue-Reading-Button>
- **Let users browse an archive by month:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Embedding-Prebuilt-Screens#Showing-an-Archive>
- **Add a row to the reader’s settings menu:**
  <doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen#Adding-Your-Own-Rows>

## Types at a Glance

Every view controller, configuration, and delegate a prebuilt app uses,
with the guide that covers it.

### View Controllers

|View controller                                                                    |Shows                                                                |Guide                                                                               |
|-----------------------------------------------------------------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController``     |The whole app: sections of archives, bookmarks, downloads, and search|<doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>       |
|``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController``      |One publication’s editions, or a kiosk of publications               |<doc://com.pagesuite.PSReader/documentation/PSReader/Embedding-Prebuilt-Screens>    |
|``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksViewController``    |The user’s bookmarked pages and articles                             |<doc://com.pagesuite.PSReader/documentation/PSReader/Bookmarks>                     |
|``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsViewController``    |Editions downloaded for offline reading                              |<doc://com.pagesuite.PSReader/documentation/PSReader/Downloads-and-Offline-Reading> |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchViewController``       |Search across your publications                                      |<doc://com.pagesuite.PSReader/documentation/PSReader/Search>                        |
|``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController``   |One edition in the prebuilt reader, opened from your own interface   |<doc://com.pagesuite.PSReader/documentation/PSReader/Presenting-the-Prebuilt-Reader>|
|``doc://com.pagesuite.PSReader/documentation/PSReader/DismissHeaderViewController``|A close button above a carousel you present                          |<doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>       |

### Configurations

|Configuration                                                                           |Configures                                                                                               |Guide                                                                              |
|----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration``             |Credentials, fonts, brand color, and delegates, for every screen                                         |<doc://com.pagesuite.PSReader/documentation/PSReader/Configuring-the-Prebuilt-UI>  |
|``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselConfiguration``           |The carousel’s ribbons, header, and navigation                                                           |<doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SectionRibbonConfiguration``      |The carousel’s section tabs                                                                              |<doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SubsectionRibbonConfiguration``   |The carousel’s subsection pills                                                                          |<doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/ButtonConfiguration``             |The close button on a ``doc://com.pagesuite.PSReader/documentation/PSReader/DismissHeaderViewController``|<doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration``            |An archive’s grid, labels, and download buttons, and the reader it opens                                 |<doc://com.pagesuite.PSReader/documentation/PSReader/Embedding-Prebuilt-Screens>   |
|``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveDatePickerConfiguration``  |An archive’s month picker                                                                                |<doc://com.pagesuite.PSReader/documentation/PSReader/Embedding-Prebuilt-Screens>   |
|``doc://com.pagesuite.PSReader/documentation/PSReader/KioskFeedPublication``            |One publication in a kiosk                                                                               |<doc://com.pagesuite.PSReader/documentation/PSReader/Embedding-Prebuilt-Screens>   |
|``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksConfiguration``          |The bookmarks screen, and the reader it opens                                                            |<doc://com.pagesuite.PSReader/documentation/PSReader/Bookmarks>                    |
|``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsConfiguration``          |The downloads screen, and the reader it opens                                                            |<doc://com.pagesuite.PSReader/documentation/PSReader/Downloads-and-Offline-Reading>|
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchConfiguration``             |Search, in its own screen or in the reader                                                               |<doc://com.pagesuite.PSReader/documentation/PSReader/Search>                       |
|``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration``             |The prebuilt reader screen and its parts                                                                 |<doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>|
|``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderNavigationBarConfiguration``|The reader’s navigation bar                                                                              |<doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>|
|``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderBrowserConfiguration``      |The reader’s content browser                                                                             |<doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>|
|``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderSplashConfiguration``       |The splash screen shown while an edition loads                                                           |<doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>|
|``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration``           |The reader’s settings menu and its defaults                                                              |<doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>|
|``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsMenuItem``                |A row of your own in the reader’s settings menu                                                          |<doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>|
|``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration``       |The audio controls shown while a page is read aloud                                                      |<doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>               |
|``doc://com.pagesuite.PSReader/documentation/PSReader/LabelConfiguration``              |The font, size, and color of one piece of text                                                           |<doc://com.pagesuite.PSReader/documentation/PSReader/Theming>                      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/ContentUnavailableConfiguration`` |The empty bookmarks and downloads screens                                                                |<doc://com.pagesuite.PSReader/documentation/PSReader/Theming>                      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/LegacyReaderConfiguration``       |The legacy replica reader                                                                                |<doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>|

### Delegates

Most are properties of your [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration), which every screen
and reader copies; a [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration) can swap one for that reader
only. A search delegate belongs to search, and an event subscriber
subscribes to [`EventChannel`](/documentation/PSReader/EventChannel).

|Delegate                                                                  |Lets you                                                                      |Guide                                                                              |
|--------------------------------------------------------------------------|------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallDelegate``   |Decide whether the user may open or download an edition, and show your paywall|<doc://com.pagesuite.PSReader/documentation/PSReader/Paywalls>                     |
|``doc://com.pagesuite.PSReader/documentation/PSReader/ShareDelegate``     |Choose what the reader’s Share button shares                                  |<doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>                      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingDelegate``|Show comment buttons on articles and open your comments                       |<doc://com.pagesuite.PSReader/documentation/PSReader/Commenting>                   |
|``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate``     |Read pages aloud from the reader’s Listen button                              |<doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>               |
|``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertDelegate``    |Supply banner adverts and advert pages from your own ad stack                 |<doc://com.pagesuite.PSReader/documentation/PSReader/Advertisements>               |
|``doc://com.pagesuite.PSReader/documentation/PSReader/MediaDelegate``     |Play videos with your own player, and customize PDF hotspots                  |<doc://com.pagesuite.PSReader/documentation/PSReader/Media-and-Links>              |
|``doc://com.pagesuite.PSReader/documentation/PSReader/AssetDelegate``     |Replace icons, the splash screen’s logo, and placeholder images               |<doc://com.pagesuite.PSReader/documentation/PSReader/Theming>                      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchDelegate``    |Choose the publications search covers                                         |<doc://com.pagesuite.PSReader/documentation/PSReader/Search>                       |
|``doc://com.pagesuite.PSReader/documentation/PSReader/EventSubscriber``   |Receive the prebuilt UI’s analytics events                                    |<doc://com.pagesuite.PSReader/documentation/PSReader/Analytics>                    |
|``doc://com.pagesuite.PSReader/documentation/PSReader/NavigationDelegate``|Follow legacy replica editions opening and closing                            |<doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>|

## Topics

### Setup

[Setting Up the Carousel](/documentation/PSReader/Setting-Up-the-Carousel)

Show the whole prebuilt UI from one view controller: your publications’ archives, bookmarks, downloads, and search.

[Embedding Prebuilt Screens](/documentation/PSReader/Embedding-Prebuilt-Screens)

Place the prebuilt archive, bookmarks, downloads, and search screens in your own navigation.

[Presenting the Prebuilt Reader](/documentation/PSReader/Presenting-the-Prebuilt-Reader)

Open an edition in the prebuilt reader from your own interface: a button, a deep link, or a push notification.

### Customization

[Theming](/documentation/PSReader/Theming)

Match the prebuilt UI to your brand: fonts, colors, dark mode, icons, placeholders, dates, thumbnails, and Liquid Glass.

[Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI)

Set the prebuilt UI’s appearance and behavior once, globally, and override it where a screen needs something different.

[Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen)

Configure the prebuilt reader’s navigation bar, content browser, splash screen, and settings menu, and add rows of your own.

[Localization](/documentation/PSReader/Localization)

Translate the prebuilt UI’s text, or replace any of its strings with your own.

### Features

[Paywalls](/documentation/PSReader/Paywalls)

Gate editions in the prebuilt UI behind your own subscription check and paywall screen.

[Downloads and Offline Reading](/documentation/PSReader/Downloads-and-Offline-Reading)

Let users download editions from the prebuilt archive, manage them on a Downloads screen, and read them offline.

[Bookmarks](/documentation/PSReader/Bookmarks)

Let users save articles and pages from the prebuilt reader, and reopen them from a Bookmarks screen, even offline.

[Search](/documentation/PSReader/Search)

Find articles and pages across your publications’ editions with the
prebuilt search screen.

[Sharing](/documentation/PSReader/Sharing)

Let users share the page or article in view from the prebuilt reader’s
share button.

[Commenting](/documentation/PSReader/Commenting)

Switch on comment buttons and counts in the prebuilt reader, and open
your commenting platform when users tap them.

[Text-to-Speech](/documentation/PSReader/Text-to-Speech)

Read articles aloud in the prebuilt reader with the SDK’s text-to-speech
provider, or bring your own voice, text, and audio controls.

[Advertisements](/documentation/PSReader/Advertisements)

Show banner adverts in the prebuilt reader, and serve its advert pages
from your own ad stack.

[Media and Links](/documentation/PSReader/Media-and-Links)

Play videos and customize PDF hotspots in the prebuilt reader, which opens
the images, embeds, and links in edition pages itself.

[Analytics](/documentation/PSReader/Analytics)

Forward what users open, view, save, and search in the prebuilt UI to
your analytics provider.

