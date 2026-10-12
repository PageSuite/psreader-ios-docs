<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25LegacyReaderConfigurationV14ShareTemplaterV"
  },
  "title" : "LegacyReaderConfiguration.ShareTemplater"
}
-->

# LegacyReaderConfiguration.ShareTemplater

Defines templated strings for customizing sharing functionality within the legacy reader.

```
struct ShareTemplater
```

## Overview

Templates may include dynamic placeholders such as `{{{HEADLINE}}}`, which are
automatically replaced by actual values at runtime. Supported placeholders include:

- `"{{{APP_NAME}}}"`
- `"{{{PUBLICATION_NAME}}}"`
- `"{{{SUBSCRIBE_URL}}}"`
- `"{{{APP_STORE_PLAY_STORE_LINK}}}"`
- `"{{{HEADLINE}}}"`
- `"{{{SHARE_LINK}}}"`
- `"{{{ARCHIVE_NAME}}}"`
- `"{{{EDITION_NAME}}}"`
- `"{{{PAGE_NUM}}}"`

## Topics

### Creating a Share Templater

[`init(popOverArticleMessageTemplate:popOverArticleSubjectTemplate:shareEditionPageMessageTemplate:shareEditionPageSubjectTemplate:subscribeUrl:publicationName:appStoreLink:)`](/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct/init(popOverArticleMessageTemplate:popOverArticleSubjectTemplate:shareEditionPageMessageTemplate:shareEditionPageSubjectTemplate:subscribeUrl:publicationName:appStoreLink:))

Initializes a new share templater with the specified template strings and URLs.

### Sharing Articles

[`popOverArticleSubjectTemplate`](/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct/popOverArticleSubjectTemplate)

Template string for the share subject of pop-over articles.

[`popOverArticleMessageTemplate`](/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct/popOverArticleMessageTemplate)

Template string for the share message of pop-over articles.

### Sharing Pages

[`shareEditionPageSubjectTemplate`](/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct/shareEditionPageSubjectTemplate)

Template string for the share subject when sharing edition pages.

[`shareEditionPageMessageTemplate`](/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct/shareEditionPageMessageTemplate)

Template string for the share message when sharing edition pages.

### Template Values

[`publicationName`](/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct/publicationName)

The publication name to be included in shared messages.

[`subscribeUrl`](/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct/subscribeUrl)

URL directing users to subscribe or purchase the publication.

[`appStoreLink`](/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct/appStoreLink)

URL to the app store page, typically included in shared messages.

