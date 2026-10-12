<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Change-Log",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Change Log"
}
-->

# Change Log

Track new features, improvements, bug fixes, and other updates in each
PSReader SDK release.

## Versioning Scheme

> Note: Starting in 2026, the SDK uses a calendar-based versioning scheme to
> align with the rest of the PageSuite product line. Versions follow the format
> **year.month.patch** — for example, `26.1.0` is the first January 2026
> release. This scheme does **not** follow semantic versioning. While we strive
> to maintain API stability, breaking changes may occur in any release without a
> major version bump. We recommend pinning to a specific version and reviewing
> this change log before upgrading.

## v26.8.0

- Merged PSReaderUI into the PSReader module. The prebuilt UI and the core
  SDK now ship as one framework, with rebuilt documentation for both.
  **Breaking change:** Replace `import PSReaderUI` with `import PSReader`
  and remove `PSReaderUI.xcframework`. The Swift package and the
  `PSReaderUI2` pod keep their names and locations.
  See: <doc://com.pagesuite.PSReader/documentation/PSReader/Migrating-From-PSReaderUI>.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionLaunch(_:)`` now carries an
  ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/FeedEditionEventContext``, which includes the opening
  page. **Breaking change:** Read the `PSEPublished` from the context.
  See: <doc://com.pagesuite.PSReader/documentation/PSReader/Analytics>.
- Removed ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageResourceName``, ``doc://com.pagesuite.PSReader/documentation/PSReader/LegacyImageResourceName``, and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey`` cases the SDK no longer requests.
  **Breaking change:** Code that names them no longer compiles.
- Added custom rows to the reader’s settings menu.
  See: ``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/additionalItems``.
- Added ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/maxContentWidth`` to cap an archive’s width
  on wide screens.
- Added ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/setRibbonLayout(section:subsectionAlignment:)``
  to change ribbon layouts after setup, for example when the window’s
  width class changes.
- Added default implementations for the replica methods of
  ``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertDelegate``, ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate``, ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareDelegate``,
  ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioSessionProvider``, and ``doc://com.pagesuite.PSReader/documentation/PSReader/TextToSpeechArticleFormatter``, so
  feed-only apps no longer need stubs for them.
- Added an async ``doc://com.pagesuite.PSReader/documentation/PSReader/initialize(apiKey:)``.
- Feed editions now show the publisher’s page names, such as “A1”, in the
  content browser, bookmarks, and page share subjects.
  **Behavior change:** Page share subjects read “(Page A1)” in place of
  “(page 1)”.
- Editions opened from a bookmark now stream, even with download while
  reading on. **Behavior change:** They previously downloaded.
- Search now requires at least three characters.
- Text-to-speech now reads headings as well as paragraphs.
- The reader’s settings menu now hides the text size option on pages
  whose text can’t be resized, such as PDF, advert, and web pages.
- Ribbons now scroll the selected item back into view when their width
  changes.
- Feed page bookmark thumbnails now have the same border as replica ones.
- Fixed a crash in ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController`` when an archive has no
  usable sections.
- Fixed downloads cancelled early in ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager`` restarting by
  themselves.
- Fixed restored editions losing their pullouts.
- Fixed PDF pages in feed editions scrolling incorrectly after rotation.
- Fixed byline authors linking to invalid email addresses.
- Legacy replica reader: Article bookmarks opened online now show the
  article over its full edition; closing the article closes the reader.
- Modern replica reader: Hides the text size option while a page spread
  is showing.
- Legacy replica reader: Fixed removing an article bookmark reporting the
  wrong analytics event. It now reports `replicaArticleBookmarkDeleted`.
- Legacy replica reader: Fixed the back button sitting under the window
  controls in windowed iPad apps on iPadOS 26.

> Note: This release introduces a new localized string key for the
> short-query message in search.
> See: ``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/searchMinimumCharacters``.

## v26.7.1

- Added date picker support to feed edition archives, previously limited to
  legacy replica archives. See: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/datePicker``.
  **Behavior change:** Dynamic archives now show the date picker for
  publications with it enabled in the PageSuite portal.

## v26.7.0

- Added support for in-flow advert pages, including the page-zero position
  beside the cover. HTML and third-party adverts render out of the box;
  Google Ad Manager adverts require a client-provided view controller.
  See: <doc://com.pagesuite.PSReader/documentation/PSReader/Advertisements#Full-Page-Advert-Pages>.
- Added search support for replica editions. See: <doc://com.pagesuite.PSReader/documentation/PSReader/Search>,
  <doc://com.pagesuite.PSReader/documentation/PSReader/Updating-the-SDK#v2670>.
- Added support for custom carousel headers with optional hide-on-scroll
  behavior. See: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselConfiguration/hidesHeaderOnScroll``.
  **Breaking change:** Replaces `CarouselConfiguration.dismissButton`.
  See: <doc://com.pagesuite.PSReader/documentation/PSReader/Updating-the-SDK#v2670>.
- Dynamic archive limits configured in the PageSuite portal are now respected.
  **Behavior change:** Portal limits were previously ignored; archives with
  a configured limit may now show fewer editions.
  See: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/archiveLimit``.
- Legacy replica reader now reopens on the last read page, matching the
  feed edition and modern replica readers.

> Note: This release introduces a new localized string key for the label shown
> above third-party advert pages.
> See: ``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/advertisementLabel``.

## v26.6.0

- Extended hide-on-swipe behavior to PDF pages and the replica reader.
  **Behavior change:** Navigation bars now also collapse on scroll in PDF
  pages and replica editions by default.
  See ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderNavigationBarConfiguration/hidesBarsOnSwipe``.
- Bookmarks now open the full edition reader when content is downloaded or the
  device is online, instead of the standalone bookmark reader. The standalone
  bookmark reader is still used when offline and the edition is not downloaded.
- Added ``doc://com.pagesuite.PSReader/documentation/PSReader/ContentUnavailableConfiguration/image`` and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/ContentUnavailableConfiguration/imageSize`` for customizing the empty-state
  icon on My Content screens.
- Fixed legacy reader article popover navigation bars not updating on color
  scheme changes.
- Fixed inconsistent sizing and centering of bookmark and download icons on
  My Content empty states.
- Fixed possible incorrect rendering of comic and puzzle pages.

## v26.5.0

- Added support for webview page types.
- Fixed potential crashes in ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechProvider`` during TTS
  playback. Synthesizer state is now serialized and the audio cache no
  longer invalidates itself on each render.
- Fixed PDF scrolling in fit-to-height mode in both the feed edition and
  replica readers. Pages now anchor to the safe area so no overflow exists
  to scroll.

## v26.4.3

- Fixed potential rendering issues on HTML advert pages.

## v26.4.2

- Adjusted default share behavior to only include URLs. Resolves issue where some
  destinations would discard the link in favor of attached images.

## v26.4.1

- Added optional `publicationName` parameter to
  ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/ContentType/feedArchive(guid:publicationName:config:)``.
- Adjusted dynamic archive publication naming logic for improved publication
  names in downloads and other UI contexts. **Behavior change:** Publication
  names may differ from previous versions. Contact support if a name needs
  adjusting.

## v26.4.0

- Added ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingCacheStrategy`` and ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingDelegate/clearCache()`` to
  control comment count freshness. See: <doc://com.pagesuite.PSReader/documentation/PSReader/Commenting#Cache-Strategy>.
- Added `pillIdealWidth` and `pillHorizontalMargin` parameters to
  ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingButton``. Reduces layout shift when comment counts update.
- Added `preferredWidth` parameter to ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentTooltipViewController``.
  See: <doc://com.pagesuite.PSReader/documentation/PSReader/Commenting#Tooltips>.
- Added ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/latestPaperThumbnailContentMode``. Fixes
  broadsheet thumbnails overflowing the archive container when using
  `flexibleHeight`.
- Updated default comment button text from “Join the conversation” to
  “View comments”.
- Fixed search cell loading skeletons. Replaced static background color
  placeholders.
- Fixed page thumbnail not shrinking in search cells.
- Fixed inconsistent date format handling in search results.
- Improved search cell loading skeletons.

## v26.3.0

- Added search functionality. See: <doc://com.pagesuite.PSReader/documentation/PSReader/Search>.
- Added commenting support. See: <doc://com.pagesuite.PSReader/documentation/PSReader/Commenting>.
- Added hide-on-swipe behavior for navigation bars in the feed edition reader.
  **Behavior change:** Navigation bars now hide on swipe by default. To disable,
  see ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderNavigationBarConfiguration/hidesBarsOnSwipe``.
- Added support for publication nameplates configurable via the PageSuite portal.
- Fixed incorrect overlay size for default TTS overlay in replica reader.
- Adjusted back navigation flow for articles in PDF-based feed editions.
  Articles now navigate back to their parent PDF page instead of dismissing
  the reader.

> Note: This release introduces new localized string keys for search and
> commenting.

## v26.2.0

- Added new sort menu to my content views.
- Added new delete all option to my content views.
- Added support for in flow article ads.
- Improved support for fixed banner ads.
- Improved placeholder image support in bookmark views.
- Fixed issue where ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechProvider`` did not read sub-headlines.
- Fixed `NSCoding` not an object warnings.

## v26.1.0

- Introduced modern replacement for the legacy replica reader.
  See: <doc://com.pagesuite.PSReader/documentation/PSReader/Updating-the-SDK#v2610>.
- Added support for custom `baseURL`s in article webviews. Resolves issues
  with embeds and relative link failures.
- Updated content browser UI for PDF pages and added page numbers.
- Added alternative UI for editions without section information. Replaces
  section ribbons with forward / back buttons.
- Improved animation when navigating to an article from PDF pages.
- Changed default `archiveLimit` (replica: 30, feed edition: unbounded).
  See: <doc://com.pagesuite.PSReader/documentation/PSReader/Updating-the-SDK#v2610>.
- Deleting all data now returns the user to the archive screen.
- Fixed incorrect share link generated when sharing bookmarked articles.
- Fixed issue with `DefaultTextToSpeechProvider` not stripping HTML from
  headlines.
- Fixed overflowing text in alerts with custom localized text.
- Fixed download button animation not correctly indicating queued state.
- Fixed grid layout issues on My Content screens on tablet. Resolves
  excessively large space between columns.
- Fixed potential crash when clearing edition data.

## v5.5.0

- Introduced Liquid Glass UI for iOS 26+. See: <doc://com.pagesuite.PSReader/documentation/PSReader/Updating-the-SDK#v550> for opt out.
- Display cached content on archive screens when offline instead of immediately
  showing the offline screen.
- Added `ImageContentMode.flexibleHeight` for archive screens.
  See: `ImageContentMode`, <doc://com.pagesuite.PSReader/documentation/PSReader/Updating-the-SDK#v550>.
- Added `locale` parameter to `DefaultEditionDateFormatter` initializer and
  defaulted it to `.current` to respect the user’s locale, aligning behavior
  with `DateFormatter`. Previously the initializer used `en_US_POSIX`.
- Automatically call global `PSReader.Initialize` function when needed to
  avoid failures if the host app forgets to initialize the SDK.
- Downgraded recommended PDFNet version to `11.5.85515` to avoid rendering regressions.
- Replica Reader: Center align PDFs in fit-to-height modes when the PDF is
  smaller than the view.
- Replica Reader: Fixed possible rendering glitch that could occur when opening
  an edition on the non-first page.
- Replica Reader: Fixed dark mode background for double page spreads.
- Replica Reader: Added analytics events for the next/previous buttons in both
  the page browser and the article browser.
- Replica Reader: Fixed possible double reporting of popover article page views.
- Replica Reader: Added a configuration option to control status bar visibility.
  See: `LegacyReaderConfiguration.prefersStatusBarHidden`.

## v5.4.0

- Added kiosk layout support for feed archives.
- Added replica supplements support.
- Added placeholder image support for page browser. See: `AssetDelegate`.
- Removed forced uppercase formatting in page browser sections.
- Fixed possible crash on bad HTML inputs.
- Fixed crash when deleting a replica article bookmark if multiple bookmarks
  originated from the same PDF page.
- Fixed possible incorrect theme on download preference prompt.
- Fixed possible missing thumbnail on bookmarks.
- Updated archive view default UI; tweaked colors and added border thumbnails.
- Enhanced settings menu with new UI and options: WiFi-Only download, print,
  auto delete downloads, clear edition data, and show page browser on first load.

## v5.3.0

- Added text-to-speech support. See: `AudioDelegate`, `DefaultTextToSpeechProvider`.
- Consolidated print into share actions. The dedicated PDF print icon has been removed.
- Added ability to print articles and section fronts.
- Updated settings UI.

## v5.2.0

- Improved handling of iPad multi tasking / split screen.
- Fixed issue where pages / articles would occasionally fail to load when
  streaming an edition.
- Added error handling for bad PDF inputs. Fixes potential crash from uncaught
  `PDFNetException`.
- Added edition sort toggle to downloads screen.
- Support for custom edition names.
- Added standalone archive view for use outside of a carousel container.
  See: `ArchiveViewController`.
- PDF pages and articles now segmented in PDF driven editions.
  See: <doc://com.pagesuite.PSReader/documentation/PSReader/Updating-the-SDK#v520>.
- Navigation bar: Removed right-side back arrow. Left icon now adapts to
  context, dismisses either the article or the reader.
  See: `ImageResourceName`, `AssetDelegate`, <doc://com.pagesuite.PSReader/documentation/PSReader/Updating-the-SDK#v520>.
- Replica Reader: Changed reader background to black in dark mode.
- Replica Reader: Fixed issue where print navigation bar item could not be enabled.
- Replica Reader: Changed default `readerBack` and `articlePopOverBack` assets.

## v5.1.1

- Fixed issue where SDK did not respond window open calls from templates.

## v5.1.0

- Dropped ZipFoundation depdendency.
- Replaced unowned references with weak references for better stability.
- Added Swift package.

## v5.0.0

- Option to read editions without downloading.
- Improved archive cache handling and offline use.
- Paywall support. See: `PaywallDelegate`.
- More fine grained date formatting. See: `EditionDateFormatter`.
- Reworked API for customizing assets. See: `AssetDelegate`.
- Added date picker support for replica archives.
- Removed bitcode from bundled `ZipFoundation.xcframework`.
- Fixed typo in `DownloadsConfiguration` type name.

## v4.3.2

- Fix issue with replica reader contents ribbon.
- Fix issue where image galleries / share sheet would not open after dismissing
  feed edition settings menu.

## v4.3.1

- Added supported screen orientations API.
- Added support for author names in article templates.

## v4.3.0

- Fix padding issue at the bottom of carousel view.
- Fix contents ribbon not tracking currently open page.
- Fix issue where reader can sometimes scroll past end of edition.
- Fix rendering issues on rotation on some templates.

## v4.2.1

- Fixed crash when swiping in legacy replica reader while offline.

## v4.2.0

- Added support for replica publication kiosks.
- Feed edition reader settings menu dark mode issues.
- Feed edition reader rotation fixes.

## v4.1.0

- Added reader settings menu.
- Added support for double page mode.
- Added fit-to-width / fit-to-height options.
- Remember last read page.

## v4.0.0

- Fixed issue with annotated links on adverts.
- Fixed issue where archive screen would disable pull-to-refresh.

## v4.0.0-preview5

- Fixed `editionDateString` timezone and format inconsistencies.
- Added edition launch analytics event when luanching from downloads.
- Added support for legal Kill scenarios.
- Fixed overrideUserInterfaceStyle regression.
- Fixed issue when swiping in carousel,
- Support for bespoke ads.

## v4.0.0-preview4

- Added support for page links.
- Fixed occasional layout issues on rotate.

## v4.0.0-preview3

- Added timezone support.
- Added support for dynamic archives.
- Added improved OOB sharing support.
- SDK globally respects `overrideUserInterfaceStyle`.

## v4.0.0-preview2

- Completed dark mode.
- Added further UI configuration options.
- Fixed back navigation logic to match web.
- Aligned PDF page names in content browser with web.
- Increased section ribbon items hit boxes.
- Fixed crash on empty edition.
- Fixed article tap + zoom gestures interfering on PDF pages.
- Removed vertical padding around PDFs.

## v4.0.0-preview1

- Renamed `feedEditionPageView` to `feedEditionOtherPageView` and ensured it
  does not fire when either a `feedEditionArticleView` or
  `feedEditionSectionView` has already been fired for a give page view.
- Added `imageResourceForName` property to `GlobalConfiguration` object as a new
  customization point for replacing icons in the SDK.
- Fixed inconsistent layouts when using `fitToHeight` thumbnails.
- Aligned UI elements with rendered `fitToHeight` thumbnail edges.
- Fixed crash when jumping to an article.