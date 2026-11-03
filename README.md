<p align="center"><img src="assets/logo.png" width="120" alt="Understand This Video For Me AI Plugin logo"></p>

# Understand This Video For Me AI Plugin

**Let any AI watch and hear a video.** Give Claude, Cursor, Grok Bot or any MCP client a local video file or a YouTube / Vimeo / Loom link, and it gets back what it can actually read:

- 8–20 **timestamped key frames** (scene changes, duplicates removed, small JPEGs)
- a **timestamped transcript** (site captions when available, otherwise local Whisper)
- one **contact-sheet image** with all frames in a grid
- one `context.md` timeline mixing what was shown and what was said

Everything runs **100% on your computer**. Your videos never leave it.

## Price
**$49 one-time. Lifetime license, up to 3 of your devices.** No subscription.
Buy: https://understandvideo.shipmonthly.com

No refunds for change of mind. If it won't work on your computer, email me within 7 days and I'll fix it or refund you.

## Install: pick your app

You need your **license key** (it's in your purchase email). Buy one at https://understandvideo.shipmonthly.com. Works on Mac and Windows.

**Step 0 for everyone: run the installer once.** It adds everything the plugin needs (ffmpeg, Python, the transcript tools), registers Claude Desktop and Cursor for you, and asks for your license key.

- **Mac**
  1. Open the [repo page](https://github.com/africaappstudio-max/understand-this-video-mcp), click the green **Code** button, then **Download ZIP**. Double-click the ZIP to unzip it.
  2. Open **Terminal** (press Cmd+Space, type *Terminal*, press Enter). Type `cd ` (with a space after it), drag the unzipped folder into the Terminal window, press Enter.
  3. Type `bash install.sh` and press Enter. When it asks, paste your license key and press Enter.
- **Windows**
  1. Same download: **Code**, **Download ZIP**, then right-click the ZIP and choose **Extract All**.
  2. Open the extracted folder, right-click `install.ps1`, choose **Run with PowerShell**.
  3. When it asks, paste your license key and press Enter.

When it says "Done", the plugin lives in `~/.video-context/app` (Windows: `C:\Users\YOURNAME\.video-context\app`). Now follow the section for your app. To activate later instead: `understand-this-video activate YOUR-KEY`.

**The path the other apps need** (replace YOURNAME with your computer user name):
- Mac: `/Users/YOURNAME/.video-context/app/bin/understand-this-video-mcp`
- Windows: `C:\Users\YOURNAME\.video-context\app\Scripts\understand-this-video-mcp.exe`

### Claude Desktop
1. Run the installer above (it registers Claude Desktop for you).
2. Fully quit Claude Desktop (Mac: Cmd+Q; Windows: right-click its icon in the tray, Quit) and open it again.
3. Start a new chat and type: `Understand this video for me: https://www.youtube.com/watch?v=zLTDLeDRrw4`. If Claude asks permission to use the plugin, click **Allow**.

**How to check it works:** open **Settings, Developer**. "Understand This Video For Me" should show as *running*. In chat, Claude answers using frames and quotes with times like `[00:21]`.

*One-click alternative (needs Python 3 and ffmpeg already installed):* download `understand-this-video.mcpb` from [Releases](https://github.com/africaappstudio-max/understand-this-video-mcp/releases/latest), double-click it, click **Install**, and paste your license key when asked.

### Cursor
1. Run the installer above (it registers Cursor for you). Restart Cursor.
2. Open **Cursor Settings** (Mac: Cmd+Shift+J; Windows: Ctrl+Shift+J), click **Tools & MCP** (or **MCP**).
3. To add it by hand instead, open the file `~/.cursor/mcp.json` (Windows: `C:\Users\YOURNAME\.cursor\mcp.json`) and paste this, using your path from above:
```json
{
  "mcpServers": {
    "Understand This Video For Me": {
      "command": "/Users/YOURNAME/.video-context/app/bin/understand-this-video-mcp",
      "args": []
    }
  }
}
```

**How to check it works:** in Cursor Settings, "Understand This Video For Me" has a green dot. In the Agent chat type `Understand this video for me: /path/to/video.mp4`.

### Claude Code
1. Run the installer above.
2. Open Terminal (Windows: PowerShell) and paste one line.
   - Mac: `claude mcp add understand-this-video -- ~/.video-context/app/bin/understand-this-video-mcp`
   - Windows: `claude mcp add understand-this-video -- "$env:USERPROFILE\.video-context\app\Scripts\understand-this-video-mcp.exe"`
3. Start `claude` and ask: `Understand this video for me: ~/Desktop/video.mp4`.

**How to check it works:** type `claude mcp list`. You should see `understand-this-video` marked **Connected**.

### Grok Bot
Grok Bot works on its own cloud computer, so it can't use a program on your laptop. You ask the Bot to set the plugin up on *its* computer. It then works on video links and on files you give the Bot (not on files that stay on your laptop).
1. Open a chat with your Bot.
2. Send this message:
   > Please install the Understand This Video For Me plugin on your own computer: run `pip install "video-context-ai[all] @ git+https://github.com/africaappstudio-max/understand-this-video-mcp.git"` (install ffmpeg first if it's missing). Then add a command (stdio) MCP server named "Understand This Video For Me" with the command `understand-this-video-mcp`. Ask me for my license key with a secure secret request (never in chat or in the command), then run `understand-this-video activate` with it.
3. When the Bot asks for the key, enter it in the secure box it shows.

**How to check it works:** ask the Bot "Which tools does Understand This Video For Me have?" It should name `understand_this_video`. Then send a YouTube link and ask what happens in it.

*Grok Build (command line):* `grok mcp add understand-this-video -- ~/.video-context/app/bin/understand-this-video-mcp`

### Windsurf, VS Code, LM Studio, Cline
Run the installer first. Then open your app's MCP settings file and paste the same block as in the Cursor section (with your path):
- **Windsurf:** click the MCP icon in the Cascade panel, then **Configure**. The file is `~/.codeium/windsurf/mcp_config.json`.
- **LM Studio:** open the **Program** tab on the right, click **Install**, then **Edit mcp.json**.
- **Cline:** click the **MCP Servers** icon, then **Configure MCP Servers**.
- **VS Code (Copilot):** press Cmd/Ctrl+Shift+P, run **MCP: Open User Configuration**, and paste this instead (VS Code uses the word `servers`):
```json
{
  "servers": {
    "Understand This Video For Me": {
      "type": "stdio",
      "command": "/Users/YOURNAME/.video-context/app/bin/understand-this-video-mcp",
      "args": []
    }
  }
}
```

**How to check it works:** the server shows as running or connected in that app's MCP list, and the app lists the tool `understand_this_video`.

### If something goes wrong
- *"License error"*: run `understand-this-video activate YOUR-KEY` (Mac: `~/.video-context/app/bin/understand-this-video activate YOUR-KEY`).
- *"ffmpeg not found"*: Mac: `brew install ffmpeg`. Windows: `winget install ffmpeg`. Then restart the app.
- *A YouTube link fails*: some videos block downloads. Download the video yourself and give the AI the file path.
- Still stuck? Email video@shipmonthly.com.

## Example prompts
1. *"Watch ~/Downloads/demo.mp4 and write the step-by-step instructions it shows."*
2. *"Summarize this YouTube video with timestamps: https://www.youtube.com/watch?v=..."*
3. *"Look at this screen recording of my bug, ~/Desktop/bug.mov, and tell me what went wrong."*

## Tool
`understand_this_video`: input `source` (file path or URL) plus optional options. Returns the frames as images, the transcript and the timeline.

## Privacy
Videos are processed locally. The only network call is the license check with Freemius. See [PRIVACY.md](PRIVACY.md).

## Support
video@shipmonthly.com

Demo video used on the website: "The Babbling Brooke" (YouTube zLTDLeDRrw4), CC BY.

Proprietary software © 2026 Ship Monthly. The source is visible, but use needs a paid license. See [LICENSE](LICENSE).
