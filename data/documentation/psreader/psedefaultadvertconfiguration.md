<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDefaultAdvertConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEDefaultAdvertConfigurationO"
  },
  "title" : "PSEDefaultAdvertConfiguration"
}
-->

# PSEDefaultAdvertConfiguration

Overridable defaults for the framework-provided advert renderer.

```
enum PSEDefaultAdvertConfiguration
```

## Topics

### Third-Party Adverts

[`loaderTemplateURL`](/documentation/PSReader/PSEDefaultAdvertConfiguration/loaderTemplateURL)

Hosted loader template used by the default advert renderer for a
third-party provider. Return nil when no hosted loader exists for
the provider — such pages render nothing unless the advert delegate
supplies a view controller. googleAdManager is deliberately nil:
GAM adverts are native-only via the delegate until a hosted GAM
loader ships.

