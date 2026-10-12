<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/init(globalConfig:carouselConfig:header:sections:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC12globalConfig08carouselF06header8sectionsAcA19GlobalConfigurationV_AA0bK0VSgSo06UIViewD0CSgSayAC11SectionItemOGtcfc"
  },
  "title" : "init(globalConfig:carouselConfig:header:sections:)"
}
-->

# init(globalConfig:carouselConfig:header:sections:)

Creates a `CarouselViewController` with the given config and content.

```
@MainActor init(globalConfig: GlobalConfiguration, carouselConfig: CarouselConfiguration? = nil, header: UIViewController? = nil, sections: [SectionItem])
```

## Parameters

`globalConfig`

Global SDK configuration object.

`carouselConfig`

Optional carousel configuration object.

`header`

Optional view controller pinned above the carousel
content. The SDK owns its layout and, when
[`hidesHeaderOnScroll`](/documentation/PSReader/CarouselConfiguration/hidesHeaderOnScroll) is `true`,
hides it as the content scrolls.

`sections`

Array of sections. See [`CarouselViewController.SectionItem`](/documentation/PSReader/CarouselViewController/SectionItem).