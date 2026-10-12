<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Edition-Platforms",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Edition Platforms"
}
-->

# Edition Platforms

Know which PageSuite system serves your editions, what that means for
your app, and why some API names say “feed” or “replica”.

## Overview

PageSuite serves editions from two systems:

- The **current edition system** serves every kind of edition: classic
  PDF editions laid out like the printed paper, responsive HTML editions,
  and editions that mix the two. Both the prebuilt UI and a custom UI
  show every edition on it. These docs call them editions, and say “on
  the current system” where the system matters.
- The **legacy replica system** is the previous generation. It serves
  classic PDF editions only, and only the prebuilt UI shows them. These
  docs call them legacy replica editions. If you call your editions
  “print replicas”, that describes the classic PDF look, which either
  system can serve; see <doc://com.pagesuite.PSReader/documentation/PSReader/Edition-Platforms#Telling-Which-System-a-Publication-Is-On>.

|             |Current system                     |Legacy replica system   |
|-------------|-----------------------------------|------------------------|
|Edition looks|Classic PDF, responsive HTML, mixed|Classic PDF             |
|Prebuilt UI  |Yes                                |Yes                     |
|Custom UI    |Yes                                |No                      |
|Identifier   |Publication GUID                   |Replica publication GUID|

“Classic PDF” and “responsive” describe how an edition looks. “Current”
and “legacy replica” describe which system serves it. A classic PDF
edition can be on either system, and on the current system it works with
a custom UI like any other edition. Many API names call the current
system “feed”, its old name; see [Historic API Names](/documentation/PSReader/Edition-Platforms#Historic-API-Names).



![The reader showing a classic PDF edition on the current system.](images/com.pagesuite.PSReader/reader-classic-pdf@2x.png)



![The reader showing a responsive edition's templated page.](images/com.pagesuite.PSReader/reader-responsive~dark@2x.png)

## Telling Which System a Publication Is On

A publication GUID and a replica publication GUID look alike, so the
value won’t tell you. The label does: PageSuite supplies a “publication
GUID” for a title on the current system and a “replica publication GUID”
for one on the legacy system. If you’re not sure which you were given,
ask your PageSuite account manager. A title that moved from the legacy
system to the current one has both, and they’re different values. See
[Identifiers](/documentation/PSReader/Identifiers).

You don’t always need to know:

- A dynamic archive, `.dynamicArchive(_:shortcode:config:)`, reads each
  publication’s system from its shortcode’s configuration and shows it the
  right way.
- With a GUID in hand, ask ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService`` for its archive. If
  editions come back, the publication is on the current system, and both
  sides can show it:
  
  ```swift
  let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
  let archive = try await service.publishedEditions(publicationGUID: "PUBLICATION_GUID")
  ```
  
  A replica publication GUID has no archive on the current system, so
  the call throws an error. An error or an empty archive doesn’t prove a
  title is legacy, though: a publication on the current system that
  hasn’t published anything yet has no editions either, and a mistyped
  GUID or the wrong account GUID throws the same error. Check with
  PageSuite before you treat a title as legacy.
- At runtime, analytics events tell the systems apart: editions on the
  current system report `feedEdition…` events, and replica editions
  report `replica…` events. See <doc://com.pagesuite.PSReader/documentation/PSReader/Analytics>.

The core SDK has no replica path. To build a custom UI for a title that’s
still on the legacy system, ask PageSuite about moving it to the current
system.

## What Differs in the Prebuilt UI

The prebuilt UI shows replica editions alongside editions on the current
system. Where they behave differently, the prebuilt guides say so in a
callout marked “Replica”. The differences, in short:

- **Archives and kiosks.** `.replicaArchive(guid:)` lists a replica
  publication’s editions, and `.replicaPublicationKiosk(publications:)`
  gathers several, each a ``doc://com.pagesuite.PSReader/documentation/PSReader/KioskReplicaPublication``. See
  <doc://com.pagesuite.PSReader/documentation/PSReader/Embedding-Prebuilt-Screens>.
- **Opening an edition directly.** ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController`` opens
  editions on the current system only. Replica editions open from the
  carousel and the prebuilt screens. See
  <doc://com.pagesuite.PSReader/documentation/PSReader/Presenting-the-Prebuilt-Reader>.
- **The reader.** Replica editions open in the legacy replica reader,
  configured through ``doc://com.pagesuite.PSReader/documentation/PSReader/LegacyReaderConfiguration``, or in the reader that
  editions on the current system use.
  ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader`` chooses; it defaults to
  the legacy reader for now and will default to the modern reader in a
  future release. See <doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen>.
- **Delegates.** The paywall, share, and audio delegates have methods for
  replica editions:
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openReplicaEdition:)``,
  ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareDelegate/shareContext(forSpread:inReplicaEdition:)``, and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate/playAudio(forSpread:inReplicaEdition:)``, among others.
  See <doc://com.pagesuite.PSReader/documentation/PSReader/Paywalls>, <doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>, and <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>.
- **Analytics.** Replica editions report `replica…` events in place of
  the `feedEdition…` ones, with their own contexts. See <doc://com.pagesuite.PSReader/documentation/PSReader/Analytics>.
- **Search.** Replica publications are searched through
  ``doc://com.pagesuite.PSReader/documentation/PSReader/ReplicaSearchService``, which finds pages only, in one publication per
  request. See <doc://com.pagesuite.PSReader/documentation/PSReader/Search>.

## Historic API Names

Some API names use older words for the systems and for the classic PDF
look. They’re part of the shipped API and stay as they are.

**“Feed” means the current system.** “Feed” is the current system’s old
name, and many of its APIs carry it. It doesn’t describe a format or a
look: [`FeedEditionService`](/documentation/PSReader/FeedEditionService) fetches a classic PDF edition as readily as
a responsive one, and [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) shows both. The same
holds for `.feedArchive` sections, [`KioskFeedPublication`](/documentation/PSReader/KioskFeedPublication),
[`FeedSearchService`](/documentation/PSReader/FeedSearchService), and the `feedEdition…` analytics events, such as
[`EventChannel.AnalyticsEvent.feedEditionLaunch(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionLaunch(_:)). Where these docs
say “feed edition”, they’re naming one of these APIs or setting the
current system against the legacy one.

**Some “replica” names mean the classic PDF look.** A few names on the
current system say “replica” for a classic PDF edition’s printed-page
look, not for the legacy system:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEdition/isReplicaEdition()`` is `true` for a classic PDF edition,
  whose PDF pages pair into facing spreads.
- A ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage`` whose ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/type`` is `replica_pdf_page` is a PDF
  page; ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/isPDF`` covers it.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionReplicaView(_:)`` fires when
  the user views a PDF page.

Everywhere else, “replica” in an API name means the legacy replica
system: `.replicaArchive(guid:)`, [`KioskReplicaPublication`](/documentation/PSReader/KioskReplicaPublication),
[`ReplicaSearchService`](/documentation/PSReader/ReplicaSearchService), [`useLegacyReplicaReader`](/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader),
the `replica…` analytics events, and the delegate methods that take a
replica edition.