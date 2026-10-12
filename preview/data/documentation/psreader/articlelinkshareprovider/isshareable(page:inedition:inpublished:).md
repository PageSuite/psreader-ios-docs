<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArticleLinkShareProvider/isShareable(page:inEdition:inPublished:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24ArticleLinkShareProviderC11isShareable4page9inEdition0I9PublishedSbAA7PSEPageC_AA10PSEEditionCAA12PSEPublishedCtF"
  },
  "title" : "isShareable(page:inEdition:inPublished:)"
}
-->

# isShareable(page:inEdition:inPublished:)

Determines whether an article-based page is shareable.
A page is shareable if it has exactly one article with a valid external share URL.

```
func isShareable(page: PSEPage, inEdition edition: PSEEdition, inPublished published: PSEPublished) -> Bool
```