# Groove-Pull

A CLI tool that turns Spotify CSV exports into a tagged offline MP3 library, with Spotify cover art and synchronized scrolling lyrics (`.lrc`).

---

## Features

- **Incremental sync**: Skips already-downloaded tracks, downloading only new additions to your CSV.
- **Spotify album art**: Queries the Spotify CDN for official 640x640 cover art and embeds it in the MP3 tags.
- **Synchronized lyrics (`.lrc`)**: Fetches timestamped lyrics from the community LRC database for scrolling display on mobile/tablet audio players.
- **Metadata tagging**: Writes standard ID3v2 frames: Title, Artist, Album, Release Year, and Genre.
- **exFAT/MTP safe naming**: Sanitizes track names and structures filenames as `Artist - Track Name.mp3` for Android/Windows filesystems.
- **Cookie support**: Reads `cookies.txt` when YouTube blocks plain requests.

---

## Requirements

- **Python 3.10+**
- **FFmpeg** (installed and available on your system `PATH`)
- Mutagen and Requests libraries

```bash
pip install mutagen requests yt-dlp
```

---

## Usage

### Simple Download
Download all tracks from the CSV to the `downloads/` directory, skipping confirmation and going straight to extraction:
```bash
python3 csv_to_mp3.py --csv playlist.csv --download --yes --no-preview
```

### Dry Run (Preview Matches)
See what YouTube videos the script will resolve and download without writing any files:
```bash
python3 csv_to_mp3.py --csv playlist.csv
```

### Advanced Options
Write to a custom folder and limit to the first 50 tracks:
```bash
python3 csv_to_mp3.py --csv playlist.csv --download --yes --no-preview --out-dir "/my/music/folder" --limit 50
```

Skip the first 100 songs (useful for manually resuming/skipping chunks):
```bash
python3 csv_to_mp3.py --csv playlist.csv --download --yes --no-preview --skip 100
```

---

## CSV Format

The script supports standard custom formats (`song` and `artist` columns) or official **Spotify Playlist Exports**:

```csv
Track Name,Artist Name(s),Album Name,Release Date,Genres,Track URI
Levitating,Dua Lipa,Future Nostalgia,2020-03-27,pop,spotify:track:3PfIrDoz19wva0Zq7V0n5w
```

*Note: For the best results, include the `Track URI` column so the script fetches 100% accurate Spotify cover art instantly.*
