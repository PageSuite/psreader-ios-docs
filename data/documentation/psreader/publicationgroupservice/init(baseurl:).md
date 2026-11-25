<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PublicationGroupService/init(baseURL:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23PublicationGroupServiceV7baseURLACSS_tcfc"
  },
  "title" : "init(baseURL:)"
}
-->

# init(baseURL:)

Creates a service.

```
init(baseURL: String = PSAPIEnvironment.current.restAPIBaseURL)
```

## Parameters

`baseURL`

Base URL of the API that serves publication
groups. Defaults to `"https://rest.api.pagesuite.app"`; pass
another only if your publication’s groups are served elsewhere.