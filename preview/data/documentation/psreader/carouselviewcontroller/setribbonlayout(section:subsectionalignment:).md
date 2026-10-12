<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/setRibbonLayout(section:subsectionAlignment:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC15setRibbonLayout7section19subsectionAlignmentyAA07SectionF13ConfigurationV0G4ModeO_AA010SubsectionfL0V0J0OtF"
  },
  "title" : "setRibbonLayout(section:subsectionAlignment:)"
}
-->

# setRibbonLayout(section:subsectionAlignment:)

Re-lays the section and subsection ribbons for a new width class without
rebuilding the carousel.

```
@MainActor func setRibbonLayout(section layout: SectionRibbonConfiguration.LayoutMode, subsectionAlignment alignment: SubsectionRibbonConfiguration.Alignment)
```

## Parameters

`layout`

The section ribbon layout to apply.

`alignment`

The subsection ribbon alignment to apply.

## Discussion

Hosts choose the layouts from their horizontal size class and call this when
it changes. A no-op when nothing changed.