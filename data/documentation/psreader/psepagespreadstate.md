<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpreadState",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEPageSpreadStateO"
  },
  "title" : "PSEPageSpreadState"
}
-->

# PSEPageSpreadState

The download state of one page spread’s assets.

```
enum PSEPageSpreadState
```

## Topics

### States

[`PSEPageSpreadState.downloading`](/documentation/PSReader/PSEPageSpreadState/downloading)

Assets are being fetched.

[`PSEPageSpreadState.downloaded`](/documentation/PSReader/PSEPageSpreadState/downloaded)

Assets are available; the spread can render.

[`PSEPageSpreadState.errored`](/documentation/PSReader/PSEPageSpreadState/errored)

The fetch failed. Ask the source to
[`retryDownload(for:)`](/documentation/PSReader/PSEPageSpreadSource/retryDownload(for:)).

