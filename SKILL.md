---
name: understand-this-video
description: Let an AI "watch" a video. Turns a local video file or a URL (YouTube, Vimeo, Loom, direct .mp4, 1000+ sites via yt-dlp) into a small set of timestamped key frames, a timestamped transcript, one contact-sheet image, and a single context.md timeline. Use whenever a user asks what a video shows, wants steps/summary/notes from a video, or asks questions about a recording or tutorial.
---

# Understand This Video For Me AI Plugin

## When to use
- The user gives a video path or link and asks about its contents (summary, steps, bugs, Q&A).
- Your model reads images and text but not video.

## Requirements
- An Understand This Video For Me licence (activated once by the installer, or `understand-this-video activate KEY`).
  Exit code 5 / "Licence error" means not activated: tell the user to activate, don't retry.
- `ffmpeg` + `ffprobe` (found on PATH or in /opt/homebrew/bin, /usr/local/bin) (macOS `brew install ffmpeg`, Ubuntu `sudo apt install ffmpeg`, Windows `winget install ffmpeg`).
- Python 3.9+. Installed by `install.sh` / `install.ps1` (ffmpeg, faster-whisper, yt-dlp).

## Command
```bash
understand-this-video "<file or URL>" --scene --out understand_this_video_output
# or, if pip-installed:  understand-this-video "<file or URL>" --scene
```
Useful flags: `--max-frames 20`, `--min-frames 8`, `--whisper-model small` (falls back to base),
`--language en` (default auto-detect), `--no-transcript`, `--no-captions`, `--wav`, `--no-audio`,
`--no-sheet`, `--cookies-from-browser chrome` (sites that block downloads), `--keep-video`.
Exit codes: 2 = ffmpeg missing, 3 = yt-dlp missing for URL, 4 = download blocked, 5 = licence.

## Reading the output (do this in order)
1. `context.md` — ONE file: header (duration, transcript source, language) and a timeline
   interleaving `FRAME frames/...jpg` lines with `[mm:ss] speech` lines. Read this first.
2. `contact_sheet.jpg` — all frames in one grid (left→right, top→bottom). Use it when your
   image budget is tight; open individual `frames/frame_NNNN_tX.Xs.jpg` for detail.
3. `transcript.txt` — `[mm:ss.ss - mm:ss.ss] text` lines (site captions for URLs when available,
   otherwise local Whisper). Absent if no audio/no transcriber.
4. `MANIFEST.json` — machine-readable: frames[{file,time_s,bytes}], language, sizes.
Answer from both visuals and speech, citing timestamps. If there's no transcript but `audio.m4a`
exists, transcribe it with whatever tool you have.

## MCP
`understand-this-video-mcp` (or `python mcp_server.py`) is a stdio MCP server with one tool,
`understand_this_video(source, out?, max_frames?, transcript?, include_images?)`.
`source` can be a path like `~/Desktop/My Video.mp4` (spaces fine, no quotes) or a URL.
