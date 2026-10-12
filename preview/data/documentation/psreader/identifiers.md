<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Identifiers",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Identifiers"
}
-->

# Identifiers

Know which identifier you have, where it comes from, and where it goes.

## Overview

PageSuite supplies an API key and an account GUID for every integration.
What else you need depends on how you load content: a shortcode for the
prebuilt UI’s dynamic archive, or publication GUIDs when you name
publications yourself. Your PageSuite account manager provides all of
them.

|Identifier              |Comes from                                                                                                                                                                         |Goes to                                                                                                                                                                                                                                                          |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|API key                 |PageSuite                                                                                                                                                                          |``doc://com.pagesuite.PSReader/documentation/PSReader/initialize(apiKey:completion:)``, ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/apiKey``                                                                                       |
|Account GUID            |PageSuite                                                                                                                                                                          |``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/accountGUID``, ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService/init(accountGUID:timeZone:)``                                                                  |
|Shortcode               |PageSuite                                                                                                                                                                          |`.dynamicArchive(_:shortcode:config:)`, ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController``                                                                                                                                         |
|Publication GUID        |PageSuite, ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/applicationGUID``, ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/applicationId``|``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService``, `.feedArchive(guid:)`, ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController``, ``doc://com.pagesuite.PSReader/documentation/PSReader/KioskFeedPublication``|
|Replica publication GUID|PageSuite                                                                                                                                                                          |`.replicaArchive(guid:)`, ``doc://com.pagesuite.PSReader/documentation/PSReader/KioskReplicaPublication``                                                                                                                                                        |
|Edition GUID            |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/editionGUID``, ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/editionId``, your own links   |``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService/published(forEditionGUID:)``, ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController``                                                                          |

> Note: The PSReaderUI docs called the publication GUID the “application
> GUID”, and the replica publication GUID the “publication GUID”.

Keep keys and GUIDs out of source control where you can, and never paste
real values into shared code or prompts. Every example in these docs uses
placeholders such as `"API_KEY"` and `"PUBLICATION_GUID"`.

## API Key

Authenticates your app with PageSuite. Pass it to
[`initialize(apiKey:completion:)`](/documentation/PSReader/initialize(apiKey:completion:)) early in your app’s launch, and to
[`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration) when you use the prebuilt UI:

```swift
PSReader.initialize(apiKey: "API_KEY")

let globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
```

[Initialize the SDK](/documentation/PSReader/Getting-Started#Initialize-the-SDK) covers initialization.

## Account GUID

Identifies your PageSuite account, which owns your publications. The
prebuilt UI takes it through [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration), and the core SDK
through [`FeedEditionService`](/documentation/PSReader/FeedEditionService):

```swift
let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
```

If you have a shortcode, its configuration names the account; see the
next section.

## Shortcode

A short code that names an app configuration in PageSuite: the
publications your app shows, their archive settings, and the reader
features they turn on. Give it to a dynamic archive and the carousel loads
everything else itself:

```swift
let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [.dynamicArchive("Editions", shortcode: "SHORTCODE")]
)
```

[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) also accepts a shortcode with an edition
GUID, and [`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate) searches a shortcode’s
publications. A shortcode is the simplest way to start, because you don’t
handle publication GUIDs at all.

A custom UI can load the same configuration with [`AppConfigService`](/documentation/PSReader/AppConfigService).
It tells you the account the shortcode belongs to, and the reader takes the
configuration for its advertising and templating settings:

```swift
let config = try await AppConfigService().configuration(forShortcode: "SHORTCODE")
guard let accountGUID = config.accountGUID else { return }

let service = FeedEditionService(accountGUID: accountGUID)
```

## Publication GUID

Identifies one publication on PageSuite’s current edition system, whether
its editions are classic PDF or responsive (see [Edition Platforms](/documentation/PSReader/Edition-Platforms)).
It’s the identifier the core SDK works from:

```swift
let archive = try await service.publishedEditions(publicationGUID: "PUBLICATION_GUID")
```

The prebuilt UI takes it in a `.feedArchive(guid:)` section, a
[`KioskFeedPublication`](/documentation/PSReader/KioskFeedPublication), and the [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController)
initializers.

To find the publication an edition belongs to, read
[`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID). Its name is a frozen API spelling for
the publication GUID, as [`applicationId`](/documentation/PSReader/SearchResult/applicationId) is on search
results. It’s empty on an edition resolved with
[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)); there, use the
publication GUID you already hold, such as the one your link or
notification carried alongside the edition GUID:

```swift
func publicationGUID(of published: PSEPublished, knownGUID: String?) -> String {
    if !published.applicationGUID.isEmpty {
        return published.applicationGUID
    }
    // Resolved from an edition GUID: use the GUID you started from.
    return knownGUID ?? published.publicationGUID
}
```

[`publicationGUID`](/documentation/PSReader/PSEPublished/publicationGUID) is the GUID the backend files the
edition’s content under, and it can differ from the publication GUID.
Use it only as a last resort, as the last line does.

## Replica Publication GUID

Identifies a publication on the legacy replica system. Only the prebuilt
UI uses it, through a `.replicaArchive(guid:)` section or a
[`KioskReplicaPublication`](/documentation/PSReader/KioskReplicaPublication). It looks like a publication GUID; what tells
them apart is the label PageSuite gave it (see
[Telling Which System a Publication Is On](/documentation/PSReader/Edition-Platforms#Telling-Which-System-a-Publication-Is-On)).

A title that moved from the legacy system to the current one has both a
replica publication GUID and a publication GUID, and they’re different
values. Use the publication GUID for anything on the current system.

## Edition GUID

Identifies one edition: a single day’s paper, or a single issue. It’s the
identifier to put in push notifications and links, because it opens an
edition directly without fetching the archive first:

```swift
let published = try await service.published(forEditionGUID: "EDITION_GUID")
```

Read it from [`editionGUID`](/documentation/PSReader/PSEPublished/editionGUID), or from a search result’s
[`editionId`](/documentation/PSReader/SearchResult/editionId). The prebuilt UI opens one with
[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController), given the publication GUID or a shortcode
alongside it; see
[Routing Links and Notifications](/documentation/PSReader/Presenting-the-Prebuilt-Reader#Routing-Links-and-Notifications). A
custom UI resolves it with
[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)); see
[Routing Links and Notifications](/documentation/PSReader/Opening-an-Edition#Routing-Links-and-Notifications).

## Identifiers Inside an Edition

The model types carry their own identifiers, which you read rather than
supply:

- **Published GUID.** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/publishedGUID`` identifies one
  catalog entry. Downloads and bookmarks are keyed by it, and so should
  anything you store per edition, such as a reading position.
- **Page, article, and section GUIDs.** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/pageguid``,
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEArticle/articleguid``, and ``doc://com.pagesuite.PSReader/documentation/PSReader/PSESection/sectionguid`` identify
  content inside an edition. Pass them to the reader’s `scrollTo` methods,
  to ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController/OpeningPage``, or to
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEdition/page(forGUID:)``.

These lowercase spellings mirror the backend payload and are part of the
shipped API. See [The Edition Model](/documentation/PSReader/The-Edition-Model) for how the types fit together.

## Topics

### App Configuration

[`PSAppConfig`](/documentation/PSReader/PSAppConfig)

The application configuration authored in the PageSuite portal, decoded
from the remote configuration payload.

