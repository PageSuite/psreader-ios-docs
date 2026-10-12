<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/GlobalConfiguration/init(apiKey:accountGUID:primaryFont:secondaryFont:brandColor:liquidGlassPolicy:timeZone:dateFormatter:shareDelegate:assetDelegate:audioDelegate:paywallDelegate:advertDelegate:mediaDelegate:navigationDelegate:commentingDelegate:remoteConfig:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19GlobalConfigurationV6apiKey11accountGUID11primaryFont09secondaryI010brandColor17liquidGlassPolicy8timeZone13dateFormatter13shareDelegate05assetU005audioU007paywallU006advertU005mediaU0010navigationU0010commentingU012remoteConfigACSS_SSSo6UIFontCAVSo7UIColorCAA06LiquidnO0O10Foundation04TimeQ0VAA011EditionDateS0_pSgAA05ShareU0_pAA05AssetU0_pAA05AudioU0_pSgAA07PaywallU0_pSgAA06AdvertU0_pSgAA05MediaU0_pSgAA010NavigationU0_pSgAA010CommentingU0_pSgAA11PSAppConfigCSgtcfc"
  },
  "title" : "init(apiKey:accountGUID:primaryFont:secondaryFont:brandColor:liquidGlassPolicy:timeZone:dateFormatter:shareDelegate:assetDelegate:audioDelegate:paywallDelegate:advertDelegate:mediaDelegate:navigationDelegate:commentingDelegate:remoteConfig:)"
}
-->

# init(apiKey:accountGUID:primaryFont:secondaryFont:brandColor:liquidGlassPolicy:timeZone:dateFormatter:shareDelegate:assetDelegate:audioDelegate:paywallDelegate:advertDelegate:mediaDelegate:navigationDelegate:commentingDelegate:remoteConfig:)

Initializes a new global configuration object with provided customization options.

```
init(apiKey: String, accountGUID: String, primaryFont: UIFont = .systemFont(ofSize: 12), secondaryFont: UIFont = .systemFont(ofSize: 12), brandColor: UIColor = .blue, liquidGlassPolicy: LiquidGlassPolicy = .automatic, timeZone: TimeZone = .current, dateFormatter: EditionDateFormatter? = nil, shareDelegate: ShareDelegate = ShareProvider(sharePolicy: .onlyArticleLink()), assetDelegate: AssetDelegate = DefaultAssetProvider(), audioDelegate: AudioDelegate? = nil, paywallDelegate: PaywallDelegate? = nil, advertDelegate: AdvertDelegate? = nil, mediaDelegate: MediaDelegate? = nil, navigationDelegate: NavigationDelegate? = nil, commentingDelegate: CommentingDelegate? = nil, remoteConfig: PSAppConfig? = nil)
```

## Parameters

`apiKey`

The API key for backend interactions.

`accountGUID`

The unique identifier for the SDK account.

`primaryFont`

The main font family used across UI elements. Defaults to `.systemFont(ofSize: 12)`.

`secondaryFont`

The secondary font family used across UI elements. Defaults to `.systemFont(ofSize: 12)`.

`brandColor`

The brand color applied throughout the UI. Defaults to `UIColor.blue`.

`liquidGlassPolicy`

Default Liquid Glass policy used throughout the SDK’s UI. Defaults to `.automatic`.

`timeZone`

Time zone used when parsing edition strings into `Date` objects. Defaults to `TimeZone.current`.

`dateFormatter`

Formatter for displaying dates in editions. Defaults to `DefaultEditionDateFormatter(timeZone: timeZone)`.

`shareDelegate`

Delegate controlling sharing functionality. Defaults to `ShareProvider(sharePolicy: .onlyArticleLink())`.

`assetDelegate`

Delegate controlling custom assets. Defaults to `DefaultAssetProvider`.

`audioDelegate`

Delegate enabling audio playback, such as text-to-speech. Defaults to `nil`.

`paywallDelegate`

Delegate controlling paywall interactions. Defaults to `nil`.

`advertDelegate`

Delegate controlling advertisement placements. Defaults to `nil`.

`mediaDelegate`

Delegate enabling video/media playback functionality. Defaults to `nil`.

`navigationDelegate`

Delegate handling custom navigation interactions. Defaults to `nil`.

`commentingDelegate`

Delegate enabling commenting functionality. Defaults to `nil`.

`remoteConfig`

The app configuration from the PageSuite portal. Defaults to `nil`.