<div align="center">
  <img src="docs/assets/logo_large_black.svg" alt="Logo" width="400">
</div>

<div align="center">
  
  ![GitHub Release](https://img.shields.io/github/v/release/AresValley/Artemis-Database)
  ![GitHub repo file or directory count (in path)](https://img.shields.io/github/directory-file-count/aresvalley/Artemis-Database/static?type=dir&label=Recognized%20Signals)
  ![GitHub Release Date](https://img.shields.io/github/release-date/AresValley/Artemis-Database?label=DB%20Latest%20Release&color=blue)

</div>

# Artemis Database

This repository stores and distributes the signal identification database for [Artemis](https://github.com/AresValley/Artemis).

> [!IMPORTANT]
>
> - **Data Distribution & Ready-to-Use Releases**: This repository serves as the distribution point for signal database assets. Ready-to-use **SQLite database files** and **media data archives** prepared for Artemis are available in the [Releases](https://github.com/AresValley/Artemis-Database/releases) section.
> - **No Crawling Scripts**: Internal parsing pipelines, verification tools, and crawler scripts are intentionally kept private to prevent automated abuse, throttling, or IP blocks on third-party servers.
> - **Human Verification**: Every dataset build undergoes manual review to verify signal parameters and metadata formatting before release.
> - **Feedback & Corrections**: If you find bugs, inaccurate parameters, or missing signals, please open an Issue.

## Repository Structure

```text
Artemis-Database/
├── static/
│   ├── index.json                      # Master index mapping page IDs to titles & versions
│   └── <pageid>/                       # Individual signal entry
│       ├── signal.json                 # Structured signal parameters, metadata & descriptions
│       └── media/
│           ├── 1.png                   # Waterfall / spectrum (FFT) snapshot (optional)
│           └── 1.ogg                   # Normalized audio recording (optional)
├── CHANGELOG.md                        # Version history and added/modified signals
└── README.md                           # This file ;)
```

## Directory & File Overview

### 1. Master Index (`static/index.json`)

The `index.json` file provides a lightweight, quick-lookup catalog of all available signals in the database without needing to parse individual signal files.

Each entry is keyed by its unique page ID:

```json
{
  "102": {
    "title": "Single Sideband Voice",
    "added_in_db": 65
  },
  "7807": {
    "title": "17067bps FSK",
    "added_in_db": 73
  }
}
```

- **`title`**: Canonical display name of the signal.
- **`added_in_db`**: Database release revision (e.g. `65`, `73`) in which the signal was first introduced.

### 2. Signal Directories (`static/<pageid>/`)

Each folder inside `static/` corresponds to a unique signal, named after its canonical numeric **`pageid`**. This ensures persistent references even if a signal's title or categorization changes.

Each directory contains:
- `signal.json`: The complete technical profile and description.
- `media/`: Accompanying spectrum images and audio recordings (if available).

#### `signal.json` Schema

A comprehensive JSON record containing physical transmission parameters, taxonomy, and textual descriptions.

#### Field Reference

| Field | Type | Description |
| :--- | :--- | :--- |
| `pageid` | `string` | Unique page ID corresponding to the directory name. |
| `title` | `string` | Primary signal name / identification label. |
| `added_since` | `integer` | Database version where this signal was introduced. |
| `spectrum` | `object` | Original spectrum asset metadata (`filename`, source `url`). |
| `audio` | `object` | Original audio recording asset metadata (`filename`, source `url`). |
| `category` | `string[]` | Taxonomic classifications (e.g., `Analogue`, `Military`, `Radar`, `Amateur Radio`, ...). |
| `frequency` | `object[]` | Characteristic center frequencies in **Hertz (Hz)** with optional descriptions. |
| `bandwidth` | `object[]` | Typical signal bandwidths in **Hertz (Hz)** with optional descriptions. |
| `acf` | `object[]` | Characteristic Autocorrelation Function peaks or pulse repetition intervals (if applicable). |
| `modulation` | `object[]` | Modulation scheme (`value`) and description (e.g. `FSK`, `PSK`, `AM`, `OFDM`, ...). |
| `mode` | `object[]` | Specific operational modes (e.g. `USB`, `LSB`, ...). |
| `location` | `object[]` | Known transmission locations or coverage (e.g., `Worldwide`, `Europe`, ...). |
| `short description` | `string` | Plain-text summary for fast previews. |
| `description` | `string` | Full technical details, background, and operational context in Markdown. |

### 3. Media Assets (`static/<pageid>/media/`)

Media files are standardized to uniform naming and container formats:

#### Waterfall / Spectrum (FFT) — `1.png`
- **Format**: Converted to standardized `.png`.
- **Purpose**: Visual identification of the RF spectrum footprint and waterfall signatures.
- **Availability**: Present for signals that include visual spectrum on the wiki.

#### Audio Samples — `1.ogg`
- **Container**: Standardized `.ogg` format.
- **Sample Rate**: Matched to the original recording's sample rate.
- **Audio Codec**:
  - `vorbis`: Used when the original audio was lossy/compressed.
  - `flac`: Used when the source audio was lossless.
- **Duration Constraint**: Capped at a maximum of **60 seconds** to keep dataset distribution sizes practical while retaining sufficient duration for audio analysis and recognition by ear.
- **Availability**: Present for signals with audible recordings.

## Releases

The raw static files in this repository serve as the source dataset. For end users and direct deployment in [Artemis](https://github.com/AresValley/Artemis), pre-compiled assets are published in the **[Releases](https://github.com/AresValley/Artemis-Database/releases)** section for every version:

- **`.tar` archives**: Bundled archives containing all normalized waterfall spectrum images (`.png`) and audio samples (`.ogg`) to enable full, standalone offline signal recognition and playback. It contains the pre-built SQLite database file matching Artemis's Peewee ORM schema (starting with Artemis 4.2.0 / DB v74). You can drop this file directly into your Artemis installation without needing to parse or ingest individual JSON files.

## Contributing & Reporting Issues

If you discover incorrect parameters, broken links, or want to suggest missing signals:
1. Check the [CHANGELOG.md](CHANGELOG.md) to see if the issue was addressed in a recent database revision.
2. Open an issue on the [Issue Tracker](https://github.com/AresValley/Artemis-Database/issues) with the signal title, and `pageid`.

## License

Artemis is licensed under the [**GPL-3.0 License**](https://github.com/AresValley/Artemis/blob/master/LICENSE).
