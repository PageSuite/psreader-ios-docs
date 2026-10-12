<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMedia",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader8PSEMediaO"
  },
  "title" : "PSEMedia"
}
-->

# PSEMedia

One media asset on a page: an article’s image or video, or an advert.

```
enum PSEMedia
```

## Topics

### Media Kinds

[`PSEMedia.image(_:)`](/documentation/PSReader/PSEMedia/image(_:))

An image.

[`PSEMedia.video(_:)`](/documentation/PSReader/PSEMedia/video(_:))

A video. The SDK doesn’t play videos itself.

[`PSEMedia.advert(_:)`](/documentation/PSReader/PSEMedia/advert(_:))

An advert from the page’s [`adverts`](/documentation/PSReader/PSEPage/adverts).

