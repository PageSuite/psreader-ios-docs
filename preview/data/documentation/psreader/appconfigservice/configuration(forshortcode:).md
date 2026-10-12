<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AppConfigService/configuration(forShortcode:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16AppConfigServiceV13configuration12forShortcodeAA05PSAppC0CSS_tYaKF"
  },
  "title" : "configuration(forShortcode:)"
}
-->

# configuration(forShortcode:)

Returns the configuration published for a shortcode.

```
func configuration(forShortcode shortcode: String) async throws -> PSAppConfig
```

## Parameters

`shortcode`

The shortcode set up in the PageSuite portal.

## Discussion

Each call fetches the configuration from PageSuite; the service
doesn’t cache it.

> Throws: ``doc://com.pagesuite.PSReader/documentation/PSReader/AppConfigServiceError/shortcodeNotFound`` when no
> configuration is published for the shortcode,
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AppConfigServiceError/invalidResponse`` when the backend rejects
> the request or the configuration can’t be read, or the underlying
> transport error.