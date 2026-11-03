<div align="center">
  <img src="docs/assets/logo_large_black.svg" alt="Logo" width="400">
</div>

<div align="center">
  
  ![GitHub Release](https://img.shields.io/github/v/release/AresValley/Artemis-Database)
  ![GitHub repo file or directory count (in path)](https://img.shields.io/github/directory-file-count/aresvalley/Artemis-Database/static?type=dir&label=Recognized%20Signals)
  ![GitHub Release Date](https://img.shields.io/github/release-date/AresValley/Artemis-Database?label=DB%20Latest%20Release&color=blue)

</div>

This repository stores the latest version of the SigId wiki database for [Artemis](https://github.com/AresValley/Artemis) and its crawler.

> [!IMPORTANT]
>
> - **Data Distribution Only**: This repository serves purely as a distribution point for pre-compiled database releases (the `.tar` archives in the releases section).
> - **No Crawling Scripts**: Internal parsing, verification tools, and API crawler scripts are intentionally kept private to prevent automated abuse, throttling, or IP blocks on third-party servers.
> - **Human Verification**: Every dataset build undergoes manual review to verify signal parameters and formatting before release.
> - **Feedback & Corrections**: If you find bugs, wrong parameters, or missing signals in the database, please open an Issue.

## Media

### Waterfall/Spectrum (FFT)

The image is converted to **png** format. The resolution is arbitrary (yet).

### Audio Sample

The standard format for an audio sample is **ogg**, with a sampling rate equal to that of the original recording. The audio codec depends on the native format:

- **vorbis**, if the original audio is compressed
- **flac**, if the original audio is lossless

To keep the total DB size within reasonable limits, the audio sample duration is limited to 1 minute (60 seconds). This is more than enough for recognition 'by ear' and analytical audio analysis.

## License

Artemis is licensed under the [**GPL-3**](https://github.com/AresValley/Artemis/blob/master/LICENSE) license.
