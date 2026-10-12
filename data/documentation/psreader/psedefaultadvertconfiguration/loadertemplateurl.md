<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDefaultAdvertConfiguration/loaderTemplateURL",
  "metadataVersion" : "0.1.0",
  "role" : "Type Property",
  "symbol" : {
    "kind" : "Type Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEDefaultAdvertConfigurationO17loaderTemplateURLySSSgAA17PSEAdvertProviderOcvpZ"
  },
  "title" : "loaderTemplateURL"
}
-->

# loaderTemplateURL

Hosted loader template used by the default advert renderer for a
third-party provider. Return nil when no hosted loader exists for
the provider — such pages render nothing unless the advert delegate
supplies a view controller. googleAdManager is deliberately nil:
GAM adverts are native-only via the delegate until a hosted GAM
loader ships.

```
static var loaderTemplateURL: (PSEAdvertProvider) -> String?
```