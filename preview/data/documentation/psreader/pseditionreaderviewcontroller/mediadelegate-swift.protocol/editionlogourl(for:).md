<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/editionLogoURL(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC13MediaDelegateP14editionLogoURL3forSSSgAA7PSEPageC_tF"
  },
  "title" : "editionLogoURL(for:)"
}
-->

# editionLogoURL(for:)

A logo image URL for templated pages, or `nil` for none (the
default).

```
func editionLogoURL(for page: PSEPage) -> String?
```

## Discussion

Page templates that show a masthead logo take it from here; the
reader doesn’t read the logo from the app configuration you pass
to [`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:)).
The prebuilt reader returns the publication’s header logo.