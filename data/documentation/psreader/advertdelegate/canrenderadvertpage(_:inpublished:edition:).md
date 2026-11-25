<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertDelegate/canRenderAdvertPage(_:inPublished:edition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14AdvertDelegateP09canRenderB4Page_11inPublished7editionSbAA7PSEPageC_AA12PSEPublishedCAA10PSEEditionCtF"
  },
  "title" : "canRenderAdvertPage(_:inPublished:edition:)"
}
-->

# canRenderAdvertPage(_:inPublished:edition:)

Reports whether [`advertViewController(forAdvertPage:inPublished:edition:)`](/documentation/PSReader/AdvertDelegate/advertViewController(forAdvertPage:inPublished:edition:))
serves a third-party advert page that has no built-in rendering: a
Google Ad Manager page, or a [`PSEAdvertProvider.custom(_:)`](/documentation/PSReader/PSEAdvertProvider/custom(_:)) one
such as Freestar or a provider only your app knows.

```
@MainActor func canRenderAdvertPage(_ page: PSEPage, inPublished published: PSEPublished, edition: PSEEdition) -> Bool
```

## Parameters

`page`

The advert page. Inspect `advertProvider`.

`published`

The published application context.

`edition`

The edition about to open.

## Return Value

`true` to keep the page, `false` to leave it out.

## Discussion

The reader asks once per such page when it opens an edition, and
leaves out every page that neither the built-in rendering nor your
delegate can render, so the user pages past it instead of seeing a
blank page. Pages the built-in rendering covers aren’t asked about,
and a reader without an advert delegate always leaves such pages
out.

The default implementation asks
[`advertViewController(forAdvertPage:inPublished:edition:)`](/documentation/PSReader/AdvertDelegate/advertViewController(forAdvertPage:inPublished:edition:)) and
returns whether it supplied a view controller, which is discarded
without being shown. That view controller must not request an ad
before [`advertPageInView()`](/documentation/PSReader/PSEAdvertContentViewController/advertPageInView()), as the
contract already requires. Implement this method to answer without
building one:

```swift
func canRenderAdvertPage(
    _ page: PSEPage,
    inPublished published: PSEPublished,
    edition: PSEEdition
) -> Bool {
    page.advertProvider == .googleAdManager
}
```