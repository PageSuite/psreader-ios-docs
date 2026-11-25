<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/isThirdPartyAdvertPage",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader7PSEPageC22isThirdPartyAdvertPageSbvp"
  },
  "title" : "isThirdPartyAdvertPage"
}
-->

# isThirdPartyAdvertPage

True for advert pages served through a third-party provider: every
`advert_third_party` page, and an `advert_html` page carrying an
advert type or config. Server feeds ship third-party adverts under
either type, as the web reader does, so the type string alone
doesn’t tell the two flows apart.

```
var isThirdPartyAdvertPage: Bool { get }
```