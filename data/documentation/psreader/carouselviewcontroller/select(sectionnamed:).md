<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/select(sectionNamed:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC6select12sectionNamedySS_tF"
  },
  "title" : "select(sectionNamed:)"
}
-->

# select(sectionNamed:)

Moves the carousel to the section, or the subsection, with the given name.

```
@MainActor func select(sectionNamed name: String)
```

## Parameters

`name`

The section or subsection name to select.

## Discussion

The name is compared with the names shown in the section and subsection
ribbons, ignoring case and whitespace, so `backissues` selects a section
named “Back Issues”. A subsection’s name selects its section and that
subsection, as does the section’s name followed by the subsection’s with a
slash between (`backissues/sunday`). In a kiosk section the same form names
one of its publications (`supplements/magazine`), whose archive opens over the
kiosk once its tiles have loaded. A name that matches nothing leaves the
carousel where it is.

Call this at any time: a selection made before the carousel is on screen is
applied once it appears, so a host can hand a deep link straight to it.

> Note: The subsections of a ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/SectionItem/dynamicArchive(_:shortcode:config:)``
> are known only once it has loaded, so a name among them matches only after that.