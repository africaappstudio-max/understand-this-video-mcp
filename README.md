<p align="center"><img src="assets/logo.png" width="120" alt="Understand This Video For Me AI Plugin logo"></p>

# Understand This Video For Me AI Plugin

**Let any AI watch and hear a video.** Give Claude, Cursor, Grok Bot or any MCP client a local video file or a YouTube / Vimeo / Loom link, and it gets back what it can actually read:

- 8–20 **timestamped key frames** (scene changes, duplicates removed, small JPEGs)
- a **timestamped transcript** (site captions when available, otherwise local Whisper)
- one **contact-sheet image** with all frames in a grid
- one `context.md` timeline mixing what was shown and what was said

Everything runs **100% on your computer**. Your videos never leave it.

## Price
**$49 one-time. Lifetime licence, up to 3 of your devices.** No subscription.
Buy: https://africaappstudio-max.github.io/video-context-ai/

No refunds for change of mind. If it won't work on your computer, email me within 7 days and I'll fix it or refund you.

## Install
**Option 1: one click (Claude Desktop).** Download `understand-this-video.mcpb` from [Releases](https://github.com/africaappstudio-max/understand-this-video-mcp/releases/latest) and open it. You need ffmpeg installed (Mac: `brew install ffmpeg`, Windows: `winget install ffmpeg`).

**Option 2: installer (Claude Desktop + Cursor, includes transcription).** Download this repo, then:
- **Mac:** `bash install.sh`
- **Windows:** right-click `install.ps1` → *Run with PowerShell*

The installer adds ffmpeg and Python if missing, installs the plugin, registers it in Claude Desktop and Cursor, and asks for your licence key.

**Other MCP clients:** add a stdio server with command `understand-this-video-mcp` (after `pip install .`), or see [`.mcp.json`](.mcp.json).

Activate: `understand-this-video activate YOUR-KEY`. Internet is needed once to activate; then it works offline.

## Example prompts
1. *"Watch ~/Downloads/demo.mp4 and write the step-by-step instructions it shows."*
2. *"Summarise this YouTube video with timestamps: https://www.youtube.com/watch?v=..."*
3. *"Look at this screen recording of my bug, ~/Desktop/bug.mov, and tell me what went wrong."*

## Tool
`understand_this_video`: input `source` (file path or URL) plus optional options. Returns the frames as images, the transcript and the timeline.

## Privacy
Videos are processed locally. The only network call is the licence check with Freemius. See [PRIVACY.md](PRIVACY.md).

## Support
africa.app.studio@gmail.com

Demo video used on the website: "The Babbling Brooke" (YouTube zLTDLeDRrw4), CC BY.

Proprietary software © 2026 Africa App Studio. The source is visible, but use needs a paid licence. See [LICENSE](LICENSE).
