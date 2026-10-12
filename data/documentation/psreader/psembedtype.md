<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEmbedType",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader11PSEmbedTypeO"
  },
  "title" : "PSEmbedType"
}
-->

# PSEmbedType

The kind of third-party embed a placeholder stands in for, as reported
by [`didTapReplacedEmbed(atIndex:originalHTML:type:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/didTapReplacedEmbed(atIndex:originalHTML:type:)).

```
enum PSEmbedType
```

## Overview

Each placeholder replaces one element of the article HTML, and the
`originalHTML` you receive is that element and its contents only. A
sibling `<script>` that loads the platform’s embed widget isn’t included,
so add one when you present the embed.

To present embeds from your own reader screen, see
[Handling Media and Link Taps](/documentation/PSReader/Handling-Media-and-Link-Taps).

## Topics

### Social Posts

[`PSEmbedType.twitter`](/documentation/PSReader/PSEmbedType/twitter)

A Twitter post: a `<blockquote>` with the `twitter-tweet` class.

[`PSEmbedType.instagram`](/documentation/PSReader/PSEmbedType/instagram)

An Instagram post: a `<blockquote>` with the `instagram-media` class.

[`PSEmbedType.tiktok`](/documentation/PSReader/PSEmbedType/tiktok)

A TikTok video: a `<blockquote>` with the `tiktok-embed` class.

### Generic Embeds

[`PSEmbedType.iframe`](/documentation/PSReader/PSEmbedType/iframe)

An `<iframe>` element.

[`PSEmbedType.embed`](/documentation/PSReader/PSEmbedType/embed)

An `<embed>` element.

