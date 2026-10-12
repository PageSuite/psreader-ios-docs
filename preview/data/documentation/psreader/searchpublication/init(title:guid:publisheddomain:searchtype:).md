<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchPublication/init(title:guid:publishedDomain:searchType:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17SearchPublicationV5title4guid15publishedDomain10searchTypeACSS_S2SSgAA0bcI0Otcfc"
  },
  "title" : "init(title:guid:publishedDomain:searchType:)"
}
-->

# init(title:guid:publishedDomain:searchType:)

Creates a new search publication.

```
init(title: String, guid: String, publishedDomain: String? = nil, searchType: SearchPublicationType = .app)
```

## Parameters

`title`

The display name of the publication.

`guid`

The publication GUID.

`publishedDomain`

The base domain for loading edition content. Pass `nil`
to use the default published domain.

`searchType`

The publication type for search queries. Defaults to `.app`.