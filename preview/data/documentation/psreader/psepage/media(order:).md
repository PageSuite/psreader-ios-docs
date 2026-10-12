<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/media(order:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader7PSEPageC5media5orderSayAA8PSEMediaOGAA12PSMediaOrderO_tF"
  },
  "title" : "media(order:)"
}
-->

# media(order:)

The page’s media: a lead asset first (the first one found among its
articles), then the page’s adverts, then the articles’ other images
and videos in the requested order.

```
func media(order: PSMediaOrder) -> [PSEMedia]
```