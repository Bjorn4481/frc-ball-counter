# FRC Ball Counter 🏀

A single-file web tool for counting scored balls in FRC YouTube videos, frame by frame.

**→ [Open the counter](https://bjorn4481.github.io/frc-ball-counter/)**

Paste a YouTube URL, play the video, tap `B` every time a ball scores. You get total balls,
average BPS, peak BPS, and a cumulative curve — no account, no upload, no database.

## How to use it

1. Paste a YouTube URL (or an 11-character video ID) and hit **Load video**.
2. The video loads at 0.25x speed, which is what you want for counting.
3. Press `B` each time a ball is scored. Shots appear in the list on the right and as
   markers on the timeline.
4. Read the stats as you go. Click any timestamp to jump back and check yourself.

### Keyboard shortcuts

| Key | Action |
| --- | --- |
| `B` | Log a ball at the current timestamp |
| `Space` | Play / pause |
| `U` | Undo the last ball |
| `[` / `]` | Seek back / forward 1 second |
| `,` / `.` | Step one frame back / forward (assumes 30 fps) |

Shortcuts are ignored while you're typing in the URL box. If the keys stop responding,
click somewhere outside the video — the YouTube iframe grabs keyboard focus when you
click it directly.

### What the stats mean

- **Total balls** — how many you logged.
- **Avg BPS** — overall throughput between the first and last ball: `balls ÷ (last − first)`.
  It ignores dead time before the first ball and after the last one.
- **Max BPS** — the best sustained 1-second burst, measured with a sliding window.
- **Duration** — length of the video, for reference.

## Running it yourself

The whole tool is one file: [`index.html`](index.html). No build step, no dependencies,
no server. Download it and open it anywhere.

⚠️ **One catch:** YouTube refuses to play embedded videos on pages opened directly from
your file system — a `file://` page gets error 153 from the YouTube player API. This is
YouTube's policy and can't be worked around in the page itself.

So either use [the hosted version](https://bjorn4481.github.io/frc-ball-counter/), or serve
your local copy over HTTP:

```bash
python -m http.server 8000
```

Then open <http://localhost:8000/>. Any http(s) address works — only `file://` is blocked.
The page detects this and tells you when it happens.

## Privacy

Nothing leaves your browser. There is no backend, no analytics, and no storage — your counts
live in the page and disappear when you close the tab. The only external request is to
YouTube, to load the video player.

## Background

This is the stripped-down, standalone version of an internal tool built by
**FRC Team 4481 Team Rembrandts** for scouting robot cycle times. The original had accounts,
leaderboards, submission verification, and a shared database behind it; this version keeps
only the counting and the statistics, so anyone can use it without signing up for anything.

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, adapt it for your team.
