<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkPage/remoteLegacyThumbnailURL()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PSEBookmarkPageC24remoteLegacyThumbnailURL10Foundation0G0VSgyF"
  },
  "title" : "remoteLegacyThumbnailURL()"
}
-->

# remoteLegacyThumbnailURL()

Remote legacy page image (the old backend’s page.jpg), used as the Saved-cell
thumbnail fallback for bridged bookmarks — their legacy edition GUID 404s on
the new render endpoint. `page.pageguid` is the legacy page id.

```
func remoteLegacyThumbnailURL() -> URL?
```