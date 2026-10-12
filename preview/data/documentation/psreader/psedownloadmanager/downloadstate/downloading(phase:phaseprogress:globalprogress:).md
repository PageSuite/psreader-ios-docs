<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/DownloadState/downloading(phase:phaseProgress:globalProgress:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC13DownloadStateO11downloadingyAeC0D5PhaseO_S2ftcAEmF"
  },
  "title" : "PSEDownloadManager.DownloadState.downloading(phase:phaseProgress:globalProgress:)"
}
-->

# PSEDownloadManager.DownloadState.downloading(phase:phaseProgress:globalProgress:)

Actively downloading. `phaseProgress` is 0…1 within the current
[`PSEDownloadManager.DownloadPhase`](/documentation/PSReader/PSEDownloadManager/DownloadPhase); `globalProgress` is 0…1 across the whole
download.

```
case downloading(phase: DownloadPhase, phaseProgress: Float, globalProgress: Float)
```