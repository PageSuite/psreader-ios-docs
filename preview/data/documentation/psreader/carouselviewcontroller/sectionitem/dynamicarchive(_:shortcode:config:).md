<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/SectionItem/dynamicArchive(_:shortcode:config:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC11SectionItemO14dynamicArchiveyAESS_SSAA0H13ConfigurationVSgtcAEmF"
  },
  "title" : "CarouselViewController.SectionItem.dynamicArchive(_:shortcode:config:)"
}
-->

# CarouselViewController.SectionItem.dynamicArchive(_:shortcode:config:)

A dynamic archive that loads publications for the given shortcode.

```
case dynamicArchive(String, shortcode: String, config: ArchiveConfiguration? = nil)
```

## Parameters

`title`

The name of the section, shown in the section
ribbon.

`shortcode`

The shortcode to load publications from.

`config`

Optional archive config object.

## Discussion

This is the recommended approach for most integrations. The shortcode is
configured in the PageSuite portal and determines which publications
and sections appear in the carousel.

```swift
.dynamicArchive("Editions", shortcode: "SHORTCODE")
```