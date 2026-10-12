<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Customizing-the-Reader-Screen",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Customizing the Reader Screen"
}
-->

# Customizing the Reader Screen

Configure the prebuilt reader’s navigation bar, content browser, splash screen, and settings menu, and add rows of your own.

## Overview

The prebuilt reader screen opens whenever the user picks an edition in
the carousel or a prebuilt screen, and whenever you present a
[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController). A [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration) sets up all of it.
Create one from your global configuration, change what you need, and give
it to whatever opens the reader:

```swift
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.backgroundColor = .black
readerConfig.navigationBar.itemSelectedBackgroundColor = .systemRed
readerConfig.settings.isDoublePageEnabled = false

var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig = readerConfig
```

Building your own reader screen? See [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader).

**iPhone:**

![The prebuilt reader showing a classic PDF edition, with callouts naming the navigation bar items.](images/com.pagesuite.PSReader/reader-classic-pdf-annotated@2x.png)

**iPad:**

![The prebuilt reader showing a classic PDF edition, with callouts naming the navigation bar items.](images/com.pagesuite.PSReader/reader-classic-pdf-ipad-annotated~dark@2x.png)

The screen shows the edition’s pages with a navigation bar on top. From
the bar, the user opens the content browser to jump between sections,
pages, and articles, and the settings menu for their reading
preferences. A splash screen covers the wait while an edition loads.

Archive, bookmarks, and downloads configurations each carry a reader
configuration at `readerConfig`, and [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) takes one
as `readerConfig`. To give every reader the same settings, share one
configuration between them; see
[Sharing One Reader Configuration](/documentation/PSReader/Configuring-the-Prebuilt-UI#Sharing-One-Reader-Configuration).

## The Navigation Bar

From the leading edge, the navigation bar holds a close button and a
Contents button, which opens the content browser. The trailing edge holds
Listen, Share, Bookmark, and Settings buttons. Some appear only when they
apply to the current page:

- **Listen** appears when your ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate`` says the page can be read
  aloud. Without one, it never appears. See <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>.
- **Share** appears when your ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareDelegate`` says the page can be
  shared. See <doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>.
- **Bookmark** appears on pages that can be bookmarked, filled in when the
  page already is.

[`ReaderNavigationBarConfiguration`](/documentation/PSReader/ReaderNavigationBarConfiguration), at
[`navigationBar`](/documentation/PSReader/ReaderConfiguration/navigationBar), styles the buttons: their label
font, background and foreground colors in the normal and selected states,
and the divider beneath the bar. By default the bar hides as the user
scrolls down through an article and returns when they scroll up; set
[`hidesBarsOnSwipe`](/documentation/PSReader/ReaderNavigationBarConfiguration/hidesBarsOnSwipe) to `false` to keep it
in place:

```swift
readerConfig.navigationBar.itemLabelFont = UIFont(name: "Georgia", size: 14)!
readerConfig.navigationBar.hidesBarsOnSwipe = false
```

The buttons’ icons come from the [`AssetDelegate`](/documentation/PSReader/AssetDelegate). Returning `nil` for a
button’s icon removes the button, which is how you drop the bookmark
button from an app without bookmarks, for example. See
[Icons](/documentation/PSReader/Theming#Icons).

## The Content Browser

The Contents button opens the content browser over the pages. It lists
the edition’s sections, with thumbnails of their pages and the articles
on them, and marks the user’s place. For a classic PDF edition, a toggle
switches between pages and articles.

**iPhone:**

![The reader's content browser listing sections, pages, and articles, with callouts for each part.](images/com.pagesuite.PSReader/reader-content-browser-annotated@2x.png)

**iPad:**

![The reader's content browser listing sections, pages, and articles, with callouts for each part.](images/com.pagesuite.PSReader/reader-content-browser-ipad-annotated~dark@2x.png)

[`ReaderBrowserConfiguration`](/documentation/PSReader/ReaderBrowserConfiguration), at [`contentBrowser`](/documentation/PSReader/ReaderConfiguration/contentBrowser),
sets its fonts and colors. Each section is drawn in the color the
edition gives it, unless you set one color for them all:

```swift
readerConfig.contentBrowser.sectionBackgroundColor = .darkGray
readerConfig.contentBrowser.sectionLabel.font = UIFont(name: "Georgia", size: 16)!
```

To open the browser automatically when an edition first loads, set
[`showContentBrowserOnFirstLoadDefault`](/documentation/PSReader/SettingsConfiguration/showContentBrowserOnFirstLoadDefault) to `true`.
Users can change it in the settings menu.

## The Splash Screen

While an edition loads, the splash screen shows its cover thumbnail, the
edition’s name and date, progress, and your logo if you supply one. If
loading fails, it shows an error the user can tap to retry.

![The splash screen shown while an edition opens, with callouts for the cover thumbnail, edition labels, and progress.](images/com.pagesuite.PSReader/reader-splash-annotated@2x.png)

[`ReaderSplashConfiguration`](/documentation/PSReader/ReaderSplashConfiguration), at [`splashScreen`](/documentation/PSReader/ReaderConfiguration/splashScreen),
styles the labels, progress bar, and error, and sets how the thumbnail
fits ([`ImageContentMode.fitToHeight`](/documentation/PSReader/ImageContentMode/fitToHeight) by default) and how the date reads
(see [Date Formatting](/documentation/PSReader/Theming#Date-Formatting)). The logo comes from your
[`AssetDelegate`](/documentation/PSReader/AssetDelegate):

```swift
struct BrandAssets: AssetDelegate {
    func headerLogo(for published: PSEPublished, currentTraitCollection: UITraitCollection?) -> URL? {
        let isDark = currentTraitCollection?.userInterfaceStyle == .dark
        return URL(string: isDark ? "https://example.com/logo-dark.png" : "https://example.com/logo.png")
    }
}
```

## The Settings Menu

The Settings button opens a menu of the user’s reading preferences:

|Row                                                |Shows when                                                                                                          |Controlled by                                                                                                                                       |
|---------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
|Text size                                          |The page has resizable text, such as an article                                                                     |                                                                                                                                                    |
|Print                                              |Always                                                                                                              |                                                                                                                                                    |
|Search                                             |The reader has a search delegate                                                                                    |``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/search``; see <doc://com.pagesuite.PSReader/documentation/PSReader/Search>|
|Reader Settings: fit to width                      |Always                                                                                                              |``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/pdfLayoutModeDefault`` sets the default                                 |
|Reader Settings: double page mode                  |``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/isDoublePageEnabled``                   |                                                                                                                                                    |
|Reader Settings: show content browser on first load|``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/isShowContentBrowserOnFirstLoadEnabled``|``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/showContentBrowserOnFirstLoadDefault`` sets the default                 |
|Data Settings: download rows                       |Each row’s own property                                                                                             |<doc://com.pagesuite.PSReader/documentation/PSReader/Downloads-and-Offline-Reading#Download-Settings-in-the-Prebuilt-Reader>                        |
|Your rows                                          |You add them                                                                                                        |``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/additionalItems``                                                       |

![The reader's settings menu, with a callout on a custom row added with a settings menu item.](images/com.pagesuite.PSReader/reader-settings-menu-annotated@2x.png)

The user’s choices are saved on the device and shared by every prebuilt
reader; the defaults apply until the user changes a setting. Hiding the
double page row or the content browser row also turns off what it
controls: no double-page spreads, or no content browser on first load.
Hiding the mobile data row only hides it; downloads over cellular stay
allowed unless the user turned them off earlier.

Data Settings holds the download rows: download while reading, mobile
data downloads, clearing edition data, and deleting old editions. The
first time the reader opens, it also asks the user whether to download
editions while reading. [Downloads and Offline Reading](/documentation/PSReader/Downloads-and-Offline-Reading) explains each
row, the question, and how to make the choice for your users.

### Adding Your Own Rows

Add a [`SettingsMenuItem`](/documentation/PSReader/SettingsMenuItem) for anything else your app needs in the
reader, such as Help or Sign Out. Rows appear after the built-in ones, in
order. A tap calls the item’s handler on the main thread with a
[`SettingsMenuContext`](/documentation/PSReader/SettingsMenuContext), which presents over the menu or closes the
reader:

```swift
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.settings.additionalItems = [
    SettingsMenuItem(title: "Help", image: UIImage(systemName: "questionmark.circle")) { context in
        context.present(HelpViewController())
    },
    SettingsMenuItem(title: "Sign Out", image: UIImage(systemName: "rectangle.portrait.and.arrow.right"), role: .destructive) { context in
        let alert = UIAlertController(title: "Sign out?", message: nil, preferredStyle: .alert)
        alert.addAction(UIAlertAction(title: "Cancel", style: .cancel))
        alert.addAction(UIAlertAction(title: "Sign Out", style: .destructive) { _ in
            context.dismissReader {
                AccountManager.shared.signOut()
            }
        })
        context.present(alert)
    }
]
```

`HelpViewController` and `AccountManager` stand for your own code. Close
the reader with [`dismissReader(animated:completion:)`](/documentation/PSReader/SettingsMenuContext/dismissReader(animated:completion:))
before leaving it, and act in the completion, as Sign Out does. The
context works only while the menu is open, so don’t keep it for later.

Give the reader configuration to every reader that should show the rows.
The archive, bookmarks, and downloads screens each open their own reader,
so set it on each of their configurations, and pass those to the
carousel’s sections or to the screens you place yourself:

```swift
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig = readerConfig

var bookmarksConfig = BookmarksConfiguration(globalConfig: globalConfig)
bookmarksConfig.readerConfig = readerConfig

var downloadsConfig = DownloadsConfiguration(globalConfig: globalConfig)
downloadsConfig.readerConfig = readerConfig

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE", config: archiveConfig),
        .subsections("My Content", [
            .init(name: "Bookmarks", type: .bookmarks(type: .all, config: bookmarksConfig)),
            .init(name: "Downloads", type: .downloads(type: .all, config: downloadsConfig))
        ])
    ]
)
```

[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) takes the reader configuration directly, as
`readerConfig`, and search opens results with the one its search delegate
supplies, such as the `readerConfig` you give an
[`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate).

## Tracking What Users Read

To know which editions users open and what they read, subscribe to the
prebuilt UI’s analytics events. The reader reports `feedEditionLaunch`
when an edition opens, then a page view for every page. See
[Analytics](/documentation/PSReader/Analytics).

## Replica Editions

> Replica: Editions on the legacy replica system can open in a different
> reader. ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader`` chooses: `true`,
> the default for now, opens the legacy replica reader, with its own
> navigation bar and icons; `false` opens the modern reader described on
> this page, so they match editions on the current system. The legacy
> reader is configured through ``doc://com.pagesuite.PSReader/documentation/PSReader/LegacyReaderConfiguration``, at
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/legacyReader``: its navigation bar buttons, share
> text templates, and status bar. Its icons come from
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AssetDelegate/legacyImageResource(for:)``. It doesn’t show
> ``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/additionalItems``. See <doc://com.pagesuite.PSReader/documentation/PSReader/Edition-Platforms>.

> Replica: ``doc://com.pagesuite.PSReader/documentation/PSReader/NavigationDelegate``, at
> ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/navigationDelegate``, reports replica editions
> only. ``doc://com.pagesuite.PSReader/documentation/PSReader/NavigationDelegate/willPresentReplicaReader()`` is called before
> a replica edition opens from an archive, in either reader, and
> ``doc://com.pagesuite.PSReader/documentation/PSReader/NavigationDelegate/willDismissReplicaReader()`` when the legacy
> replica reader closes.

## Topics

### Reader Configuration

[`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration)

Configuration object for customizing the prebuilt reader.

### Navigation Bar

[`ReaderNavigationBarConfiguration`](/documentation/PSReader/ReaderNavigationBarConfiguration)

Configuration object for customizing reader navigation bars.

### Content Browser

[`ReaderBrowserConfiguration`](/documentation/PSReader/ReaderBrowserConfiguration)

Configuration object used to customize the appearance of the reader content browser.

### Splash Screen

[`ReaderSplashConfiguration`](/documentation/PSReader/ReaderSplashConfiguration)

Configuration object for customizing the splash screen displayed when opening
a published edition. The splash screen provides visual feedback during content
loading transitions, displaying the edition’s thumbnail, name, date, loading status.

### Settings Menu

[`SettingsConfiguration`](/documentation/PSReader/SettingsConfiguration)

Configuration object used to customize the reader’s settings menu.

[`SettingsMenuItem`](/documentation/PSReader/SettingsMenuItem)

A row your app adds to the reader’s settings menu.

[`SettingsMenuContext`](/documentation/PSReader/SettingsMenuContext)

Lets a settings menu item’s handler present over the menu, or close the
menu and the reader beneath it.

### Replica Editions

[`LegacyReaderConfiguration`](/documentation/PSReader/LegacyReaderConfiguration)

Configuration object for customizing the appearance, behavior, and sharing
strategies of the legacy replica reader.

[`NavigationDelegate`](/documentation/PSReader/NavigationDelegate)

A delegate for the prebuilt UI’s replica reader lifecycle.

