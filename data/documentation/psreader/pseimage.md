<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEImage",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEImage"
  },
  "title" : "PSEImage"
}
-->

# PSEImage

An article image with its crops, caption, and credit.

```
@objc class PSEImage
```

## Topics

### Loading the Image

[`URLs`](/documentation/PSReader/PSEImage/URLs)

Where to load the image from, in order of preference: the main image,
a smaller rendition when there is one, then [`originalURL`](/documentation/PSReader/PSEImage/originalURL).

[`originalURL`](/documentation/PSReader/PSEImage/originalURL)

The image’s absolute URL, when the backend sends one. [`URLs`](/documentation/PSReader/PSEImage/URLs)
includes it.

[`thumbnailImage`](/documentation/PSReader/PSEImage/thumbnailImage)

URL of a thumbnail of the image, when the backend sends one.

[`crops`](/documentation/PSReader/PSEImage/crops)

Fixed aspect-ratio crops of the image, when the backend supplies them.

### Caption and Credit

[`imagecaption`](/documentation/PSReader/PSEImage/imagecaption)

The image’s caption.

[`imagecredit`](/documentation/PSReader/PSEImage/imagecredit)

The image’s credit or copyright line.

### Role

[`isLeadAsset`](/documentation/PSReader/PSEImage/isLeadAsset)

Whether the image is its article’s lead asset.

[`isAdvert`](/documentation/PSReader/PSEImage/isAdvert)

Whether the image is an advert rather than editorial imagery.

[`link`](/documentation/PSReader/PSEImage/link)

A link for the image, when the backend sends one.

