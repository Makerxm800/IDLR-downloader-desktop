# ⚡ IDLR — Internet Downloader

**Your personal, self‑hosted media download hub.**
Paste any link, and IDLR grabs the video or audio you want — no ads, no redirects, no third‑party uploads.
Everything runs locally on your machine.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![yt‑dlp](https://img.shields.io/badge/yt--dlp-latest-orange)
![spotdl](https://img.shields.io/badge/spotdl-latest-brightgreen)

> **Current version: v1.6.0** — now available as a desktop app, with Windows, Linux and macOS build targets.

---

## ✨ Features

- 🌐 **1000+ supported sites** via `yt‑dlp` – YouTube, TikTok, Instagram, Twitch, HLS / movie streams, and more
- 🎵 **Spotify audio** – tracks, albums & playlists via `spotdl`, with automatic YouTube-match fallback when Spotify's API misbehaves (format + bitrate respected)
- 🔍 **Live URL detection** – paste a link and the UI instantly recognises the platform (+ optional auto‑set of Mode/Format)
- 🖼️ **Thumbnail preview + Thumbnail button** – see title, uploader, duration & cover before you download, or save just the cover art with one click
- 🎛️ **Settings toggles that actually work** – every switch changes real behaviour (see table below)
- 🎨 **6 themes + Liquid Glass** – Midnight, Light, Ocean, Sunset, Forest, Rosegold, like Nebula Cloud (kept small on purpose)
- ℹ️ **Premium Info panel (ⓘ)** – live app / yt‑dlp / FFmpeg versions, network URL, save folder, supported sites
- 📋 **Bulk history management** – search, select, rename ✏️, re-download, star ★ favorites, or move to 🗑 Trash (restore / empty)
- 🖥️ **Honest terminal output** – `python app.py` shows setup, per‑download progress, `DONE` / `FAILED` reasons
- 🔒 **100% private** – accounts, history & settings live in `~/.idlr_app/` on your PC only

---

## 🧩 Supported Platforms

| Platform | Video | Audio | Notes |
|----------|:-----:|:-----:|-------|
| YouTube  | ✅    | ✅    | Playlists supported |
| Spotify  | —     | ✅    | Via `spotdl`, MP3/M4A/OPUS/FLAC |
| SoundCloud | —  | ✅    | Auto‑switches to Audio |
| TikTok   | ✅    | ✅    |  |
| Twitter/X| ✅    | ✅    |  |
| Instagram| ✅    | ✅    |  |
| Twitch   | ✅    | ✅    | Clips & VODs |
| Vimeo    | ✅    | ✅    |  |
| Facebook | ✅    | ✅    |  |
| Reddit   | ✅    | ✅    |  |
| Dailymotion | ✅ | ✅    |  |
| HLS / `.m3u8` streams | ✅ | ✅ | Merged via FFmpeg |
| Direct `.mp4/.mkv/.webm` files | ✅ | ✅ | Downloaded directly |
| + 1000 more via `yt‑dlp` | ✅ | ✅ | Generic extractor fallback |

---

## 🚀 Quick Start

### Desktop App

IDLR opens in its own desktop window by default. The same app and its existing features are included in the packaged builds. The desktop server binds only to localhost on port 5000, keeping saved browser preferences on a stable origin.

- **Windows:** build `dist/IDLR.exe` on Windows.
- **Linux:** build `dist/IDLR` on Linux. The target machine needs GTK 3 and WebKit2GTK 4.1.
- **macOS:** build `dist/IDLR.app` on macOS. Builds are unsigned; macOS may require you to right-click the app and choose **Open** the first time.

Build on the operating system you want to run on (PyInstaller does not cross-compile):

```bash
python -m pip install -r requirements-build.txt
python build.py
```

The Spotify helper is packaged beside the app. Keep both `IDLR` and `IDLR-spotdl` together on Windows/Linux; on macOS it is included inside `IDLR.app`.

Tagged pushes and manual runs of **Build desktop apps** in GitHub Actions produce separate Windows, Linux and macOS artifacts. They must be built on their target operating system. A system FFmpeg is recommended for audio conversion and video merging.

### Prerequisites

- Python 3.10 or newer
- `ffmpeg` recommended (required for MP3 extraction, video merging & thumbnails).
  The app ships `static-ffmpeg` as a fallback, but a system FFmpeg is more reliable.

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/idlr.git
cd idlr

# 2. Create a virtual environment (recommended)
python -m venv venv

# macOS / Linux
source venv/bin/activate

# Windows
venv\Scripts\activate

# 3. Install app and desktop-window dependencies
pip install -r requirements.txt

# 4. Install ffmpeg (if not already present)
# macOS:
brew install ffmpeg
# Ubuntu/Debian:
sudo apt install ffmpeg
# Windows:
winget install ffmpeg
```

### Run

```bash
python app.py
```

IDLR opens in a desktop window. Use `python app.py --browser` to run it in your browser on this PC, or `python app.py --network` to allow devices on your Wi-Fi to connect.

---

## 🖥️ Usage

1. **Paste a URL** into the main input – the platform badge appears automatically.
2. **Select Mode / Quality / Format** from the dropdowns (or let Auto‑detect set them).
3. **Click “Download Now”** – watch live progress in the app console. Browser/terminal mode also shows backend logs. Or click **“🖼 Thumbnail”** to save just the cover art.
4. **Track everything in History** – tabs for Files / ★ Favorites / 🕘 Recent / 🗑 Trash. Search, rename ✏️, re‑download ↺, star ★, or delete (goes to Trash, restorable).
5. **Customise via Settings** (gear icon) – every toggle takes effect immediately.
6. **Need help?** Click the **ⓘ Info button** for versions, system status & supported sites.

---

## ⚙️ Configuration

All settings live in the in‑app Settings panel (gear icon). They save to your browser instantly.

| Setting | Default | What it actually does |
|---------|---------|----------------------|
| Theme | Midnight | 6 themes: Midnight, Light, Ocean, Sunset, Forest, Rosegold. Saved per device (`idlr_theme`), applied before first paint (no flash) |
| Liquid Glass | ON | Frosted blur on cards, modals & topbar (Nebula-style). OFF = solid surfaces, faster paint |
| Auto‑detect URL | ON | Auto‑switches Mode/Format on paste (e.g. Spotify → Audio/MP3). OFF = badge only, your options stay untouched |
| Download Thumbnail | ON | Embeds & saves cover art. OFF = no `writethumbnail`/`EmbedThumbnail`, faster + fewer FFmpeg failures |
| Link Preview | ON | Fetches title, uploader, duration & cover on paste. OFF = no auto preview calls |
| Full Playlist | OFF | ON = downloads the whole playlist even in single Video/Audio mode (`noplaylist=false`) |
| Download Alerts | ON | Bell notification when a download finishes or fails. OFF = silent |
| Confirm Before Delete | ON | Asks before bulk/clear history deletes. OFF = delete immediately |
| Hero Animations | ON | Animated hero title + chips. OFF = static, instant (adds `no-anim` to page) |
| Calm Motion | OFF | ON = minimises all animations site-wide (accessibility, `reduce-motion`) |
| Console Log | ON | Live download output under the progress bar. OFF = console hidden (`hide-console`) |
| Save Login Session | ON | Keeps you signed in across restarts (`localStorage`). OFF = session cleared on login |
| Save folder | `~/Downloads` | Where finished files go. Click the path bar to change |
| Update yt‑dlp + spotdl | — | One‑click updater in Python/browser mode; packaged desktop builds use a newer IDLR release for bundled updates |

> The panel is responsive: bottom-sheet on phones (≤560px), 2-column grid on tablets/desktops.
> Every row shows its live state (e.g. “ON — cover art embedded”), toggles are keyboard-friendly (Enter/Space), and switches animate with a spring knob + glow.

> All data (accounts, history) is stored locally in `~/.idlr_app/` (`accounts.json`, `history.json`).
> Nothing is ever sent anywhere except the download request to the source site.

---

## 🗂️ Project Structure

```text
idlr/
├── app.py        # Flask backend (API, downloads, auth, history)
├── index.html    # Full frontend (single file: HTML + CSS + JS)
├── favicon.svg   # App icon
├── spotdl_worker.py # Bundled Spotify CLI entry point
├── build.py      # PyInstaller build for the current OS
├── requirements.txt
├── requirements-build.txt
├── .github/workflows/desktop-build.yml
└── README.md     # This file
```

The app keeps its accounts and history in `~/.idlr_app/`. Packaged builds include the frontend, backend dependencies and Spotify helper.

### Key API endpoints

| Method | Endpoint | Purpose |
|--------|----------|---------|
| POST | `/api/register` · `/api/login` · `/api/google-login` | Auth |
| POST | `/api/profile` · `/api/prefs` | Profile + download prefs |
| POST | `/api/delete-account` | Permanently delete account + history |
| POST | `/api/download` | Start a download (`thumb`, `playlist_all` respected) |
| GET  | `/api/progress/<job_id>` (SSE) | Live progress stream |
| POST | `/api/preview` | Title / thumbnail / duration lookup |
| POST | `/api/thumbnail` | Download cover art only (YouTube via yt-dlp, Spotify via oEmbed), saved to save folder + history |
| GET  | `/api/history` | History (with `starred` / `trashed` flags) |
| DELETE | `/api/history/clear` | Move ALL entries to Trash (restorable) |
| DELETE | `/api/history/remove` | Move entry to Trash (restorable) |
| POST | `/api/history/restore` · POST `/api/history/delete` · DELETE `/api/history/empty-trash` | Restore / delete forever / empty trash |
| POST | `/api/history/star` | Toggle favorite ★ |
| POST | `/api/history/rename` | Rename a history entry ✏️ |
| GET  | `/api/info` | Versions (`version`, `ytdlp`, `ffmpeg`), network URL |
| POST | `/api/update-ytdlp` | Upgrade yt‑dlp + spotdl |

---

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| `ffmpeg not found` / merge fails | Install FFmpeg and restart the terminal. Or turn **Download Thumbnail OFF** for aqueicker, less fragile download |
| YouTube `403` / `Sign in to confirm` | Settings → **Update yt‑dlp + spotdl**, then retry. Age‑restricted / DRM content cannot be downloaded |
| Spotify download fails with `KeyError: 'uri'` / traceback | Spotify changed their private API and broke spotdl's lookup. IDLR now auto-falls back to a YouTube audio match — just retry the download. If title lookup is also blocked, paste the YouTube link for the song directly |
| Spotify download fails | Make sure the link is public. Check bitrate/format choice. Terminal shows the exact reason and which engine was used |
| `app.py` crashes on startup with a `pydantic`/`SystemError` wall of text | A library update clashed versions (spotdl's `pydantic-core` mismatch). The app starts in degraded mode if Spotify cannot load. In Python mode, Settings can update the dependency pair together; packaged desktop builds need a newer IDLR release. Manual repair: `python -m pip install -U pydantic pydantic-core spotdl` |
| `No downloadable video found` | The page has no direct media (login wall, JS‑only player, or DRM like Netflix) |
| Save folder not writable | Pick an existing folder via the path bar; the backend creates it and probe-writes before starting, so you get the reason up front instead of mid-download |
| `Postprocessing: Error opening output files: Invalid argument` | The video title ends with a dot or has characters Windows forbids (`Thank you and Goodbye.` → `..mp4`). Fixed: all filenames are now Windows-sanitised (trailing dots/spaces, illegal chars, reserved names, over-long paths) on every site |
| `Permission denied: 'C:\WINDOWS\system32\tmp...tmp'` | Your process temp folder points somewhere Windows blocks (often from launching inside System32 or a broken TEMP var). Fixed: yt-dlp temp is now pinned to a verified-writable dir (`~/.idlr_app/tmp`), preview/metadata calls too. Restart `python app.py` from your normal folder (not System32) and you're set |
| Toggles “do nothing” | Fixed in v1.1.0 — every toggle now applies instantly + persists. Hard‑refresh (`Ctrl+Shift+R`) if you still see the old UI |
| Update button seems dead | In Python/browser mode it shows update progress and needs `app.py` running. Packaged desktop builds use newer IDLR releases for bundled updates |
| Desktop app does not open | Check `~/.idlr_app/idlr.log`; Windows needs the Microsoft Edge WebView2 Runtime, and Linux needs GTK 3 + WebKit2GTK 4.1 |
| Rename / Delete Account 404 | Fixed in v1.1.0 — backend now implements both endpoints |

---

## 📜 Changelog

### v1.6.0 — desktop app + multi-platform builds

- IDLR now opens in its own desktop window, using a loopback-only local server on port 5000 so saved browser preferences persist between launches; browser and Wi-Fi sharing remain available with `--browser` and `--network`.
- Added a PyInstaller build for Windows, Linux and macOS, plus a GitHub Actions workflow that builds each target on its native OS.
- Packaged a separate Spotify CLI helper so Spotify track, album and playlist downloads remain available in frozen desktop builds.
- Packaged builds update through newer IDLR releases instead of trying to modify bundled Python libraries in place.

### v1.5.0 — one file per download + Favorites & Trash

- **One download = one file:** fragment/`.part` sidecars are auto-removed when a job finishes or fails, and every new download sweeps legacy junk — the old `..f616` double-dot leftovers and 24h-stale `.part` files (your screenshot). Delete the big leftovers once by just starting any download.
- **Favorites ★ + Trash 🗑:** History now has Files / Favorites / Recent (7 days) / Trash tabs with counts. ★ pins favorites, 🗑 moves to Trash (restorable, Restore All), Empty Trash deletes forever. Clear All now moves to Trash instead of wiping.
- **Quiet refresh:** “Welcome back” greetings + notifications fire only on fresh sign-in, never on reload. Notifications capped at 50 so the list stays meaningful.
- **BETA pill** next to the IDLR logo (topbar + login), subtle hover sheen on settings rows and theme cards. Toggles untouched — all still work.

### v1.4.1 — merge-failure fix (“Error opening output files”)

- **What you saw:** download ran, “Merging video + audio…”, then `X ERROR: Postprocessing: Error opening output files: Invalid argument` — on YouTube and potentially any site.
- **Root cause:** titles ending with a dot (`Thank you and Goodbye.` → `Thank you and Goodbye..mp4`) are illegal on Windows, so ffmpeg couldn't open the output. Proven by printing the generated filename; `--windows-filenames` does NOT strip this in current yt-dlp.
- **Fix:** new `_SafeDL` layer sanitises every output name after yt-dlp prepares it — trailing dots/spaces, illegal chars, reserved names (`CON`, `NUL`…), over-long paths. Applies to downloads, merges and thumbnails on all sites.
- **Proven live:** your exact video downloaded + merged → `Thank you and Goodbye.mp4` on disk.
- Also: ANSI color codes (`[0;31m…`) no longer leak into the app's error lines.

### v1.4.0 — Spotify fallback + Shorts (tested with real downloads)

- **Spotify fixed for real:** Spotify's private API now returns `GenericError`, breaking spotdl's track lookup (`KeyError: 'uri'`) — plus spotdl couldn't find FFmpeg on its own. Fixed both: spotdl gets our FFmpeg path explicitly, and when it still fails IDLR auto-falls back to a YouTube audio match (title via public oEmbed → `ytsearch1:` → same MP3 pipeline with your format/bitrate). Proven live: `spotdl FAILED → Fallback match → DONE → .mp3 on disk`.
- **Shorts verified:** `/shorts/` links download end-to-end (metadata → fragments → merge → `.mp4`). Proven live: `Me at the zoo.mp4` saved. Paste badge now says “YouTube Short detected — vertical video”.
- YouTube watch/music extraction re-verified (incl. 4K), search-result titles/thumbs now resolve to the actual match instead of the query string.

### v1.3.2 — “failed fetch / Permission denied system32” fix

- **What you saw:** every download + preview failed with `Permission denied: 'C:\WINDOWS\system32\tmp....tmp'`, and the save bar showed a literal `%USERPROFILE%\Downloads`.
- **Root causes:** (1) yt-dlp trusted the machine's ambient temp folder, which on your setup resolves into `System32` where writes are blocked; (2) the frontend displayed a `%USERPROFILE%` placeholder that Windows never expands, and old copies of it could even be saved as the real path.
- **Fixes:** yt-dlp `temp` is now pinned to a verified-writable dir (`~/.idlr_app/tmp`, probe-written at use) for downloads, metadata, preview and thumbnail fetches; save folder is `%VAR%`/`~`-expanded, created, and probe-written *before* a job starts (clear 400 error up front, no more mid-download `✗`); `/api/info` now serves the real `default_path` which the UI displays; legacy `%…%` values in saved settings are discarded; `Errno 13` maps to a human message telling you to relaunch outside System32.
- Launch `python app.py` from your normal folder (not `C:\Windows\System32`) and paste the link again.

### v1.3.1 — startup crash guard (“doesn't work anymore” fix)

- **What happened:** an update pulled mismatched helper libraries (`pydantic` 2.13.5 vs `pydantic-core` 2.49.0), so `import spotdl` exploded and `app.py` died on startup with a scary traceback. Nothing was hacked — just a version clash.
- **Repaired your PC:** matched pair reinstalled (`pydantic-core` 2.46.5), `import spotdl` verified working.
- **So it can never kill the app again:** startup check now catches *any* import failure (was `ImportError` only), self-repairs, and if the optional Spotify engine is still broken it starts anyway with a `[WARN]` — YouTube etc. keep working, Spotify shows the exact repair command instead of a traceback.
- **Root cause fixed:** Settings updater now upgrades `pydantic` + `pydantic-core` together with `spotdl`, which is the combination that caused the clash.
- Friendly-error map + degraded-mode path tested live (broken-engine simulation → clean `error` job with repair instructions).

### v1.3.0 — thumbnail button + notification & dropdown fixes

- **New — 🖼 Thumbnail button:** next to Download Now. Saves only the cover art (YouTube etc. via yt-dlp metadata, Spotify via public oEmbed — no auth). Sanitised filename, no-overwrite numbering, 15 MB cap, history entry (`Thumbnail` mode gets its own row per link), terminal `[THUMB]` logs, respects Download Alerts.
- **Fixed — notifications in Light mode:** popover + items were stuck dark. Remade premium: icon bubbles per type (success/error/info/update), count pill in header, staggered entrance, hover slide, friendlier empty state — all theme-aware.
- **Fixed — dropdown sliding under next card (your screenshot):** Liquid Glass blurred `.card`, and blur creates a stacking context that trapped the open Mode/Quality/Format menu underneath the Save Location card. Cards are now never blurred (their `var(--card)` is near-opaque anyway) — blur stays on modals, popovers, topbar and the dropdown itself. Also removed a mobile `overflow-x` on the topbar that could clip the notification popover.
- History dedupe now keys on `(user, url, mode)` so a thumbnail save no longer overwrites the video row for the same link.

### v1.2.0 — themes + settings glow-up

**New — themes (Nebula-style, small set)**

- 6 themes: **Midnight** (default), **Light**, **Ocean**, **Sunset**, **Forest**, **Rosegold** — `body[data-theme]` variable overrides, saved as `idlr_theme`, applied before first paint (no white flash).
- **Light theme** done properly: dark text + tinted surfaces, not just inverted vars.
- Accent color (`--red`) follows the theme, so toggles, buttons, badges and glows all match.

**New — 5 more toggles (all functional)**

| Toggle | Default | Effect |
|--------|---------|--------|
| Link Preview | ON | OFF = no auto title/cover fetch on paste |
| Download Alerts | ON | OFF = no bell notification on done/failed |
| Confirm Before Delete | ON | OFF = bulk/clear history deletes skip `confirm()` |
| Liquid Glass | ON | OFF = solid surfaces, faster paint (`body.liquid-glass`) |
| Calm Motion | OFF | ON = site-wide animation kill (`body.reduce-motion`, accessibility) |

**Redesigned — Settings GUI**

- Fits every device: bottom-sheet on phones (≤560px, safe-area padding), auto-fit grid on tablets/desktops, `86–92dvh` scrolling, `clamp()` padding.
- Better info: each row has a live status dot + sub-text describing its CURRENT state (updates on every flip).
- Animation: spring knob (`cubic-bezier(.34,1.8,.64,1)`), glow pop on enable, hover grow, press squash, keyboard support (Tab + Enter/Space, `role="switch"`, focus rings).
- Theme picker: swatch cards with active ring + check, same interaction language as Nebula Cloud.
- Small global mobile fit: wrapping topbar, full-width Download button, single-column options.

### v1.1.0 — reliability + honest UI update

**Fixed — downloads**

- **Spotify fixed:** removed the fragile `Song.from_url` Python‑API import that crashed on newer `spotdl` versions; now uses the stable `python -m spotdl` CLI only, respects your **format + bitrate** (96–320k), mirrors progress to the app console, and saves history on success *and* failure.
- **Video fixed:** thumbnails are now conditional (`Download Thumbnail` toggle) instead of forced `EmbedThumbnail` (which used to fail whole downloads when FFmpeg/thumb was missing); **audio bitrate choice is respected** (`FFmpegExtractAudio` quality from your `320k/256k/…` pick); direct HLS/`.mp4` handling kept; `noplaylist` now honours the **Full Playlist** toggle.
- **Clear errors:** raw `yt‑dlp`/`spotdl` tracebacks are translated (`403`, private video, age‑restricted, DRM, timeout, missing FFmpeg…) in both the app console and terminal.

**Fixed — missing backend (frontend called them, server 404'd)**

- Added `POST /api/history/rename` (History ✏️ button works again).
- Added `POST /api/delete-account` (Settings → Delete Account works again).
- Fixed Settings updater row (it looked for `#sp-update-title`/`#sp-update-sub` that didn't exist — ids added, Updating…/Updated ✓ states visible).
- `/api/info` now also returns `version` + `ffmpeg_path`.

**Fixed — premium toggles (“didn't change anything”)**

| Toggle | Before | After |
|--------|--------|-------|
| Auto‑detect URL | Always auto‑switched options | OFF = badge only, your Mode/Format untouched |
| Download Thumbnail | Ignored | Sent as `thumb` → backend skips thumbnail steps |
| Full Playlist | Ignored (`"Playlist" in mode` only) | Sent as `playlist_all` → forces full‑playlist download |
| Hero Animations | Ignored | Toggles `body.no-anim`, kills/re‑enables animations + toast feedback |
| Console Log | Ignored | Toggles `body.hide-console`, hides/shows console + toast |
| Save Login Session | Partly worked (DOM race) | Uses settings state directly; session set/cleared reliably |

**Better Info (ⓘ)**

- Rebuilt from a 2‑line stub into a premium card: hero + version badge, live **App / yt‑dlp / FFmpeg** stats, *What it does* guide, supported‑source chips, **System status** rows (network URL, save folder), then Legal & Support.
- **What’s New** popup rewritten to describe these real changes and re‑shown once for existing users.

**Better terminal (`python app.py`)**

- Old: 6 plain lines, silent installs, zero download output.
- New: ASCII‑safe startup banner (version, Python, yt‑dlp, local + network URLs, FFmpeg status, data dir, how to read downloads), `[SETUP]` dependency lines, and per‑download logs: `[DL] NEW …`, `[YT-DLP]/[SPOTIFY] … Found / Downloading / DONE -> folder / FAILED: reason`, `[UPDATE]`, `[HIST]`, `[AUTH]` lines. Safe on Windows `cp1252` consoles.

**Docs**

- README rewritten: correct install (no phantom `requirements.txt`/`static/`/`templates/`), accurate settings table, endpoint list, expanded troubleshooting, and this changelog.

### v1.0.0 — initial release

- Flask + single‑file UI, auth, history, notifications, YouTube/Spotify/SoundCloud/TikTok/Instagram/Twitch support, HLS handling, settings panel shell, About/Terms/Privacy/Cookies modals.

---

## 🤝 Contributing

This is a personal self‑hosted project, but contributions are welcome!
If you find a bug or have a feature request, please open an issue or submit a pull request.

## 📄 License

Distributed under the MIT License. See the `LICENSE` file for more information.

## 🙌 Acknowledgements

- `yt‑dlp` – the powerhouse behind media extraction
- `spotdl` – for seamless Spotify audio
- `Flask` – the lightweight web framework
- `FFmpeg` – for audio/video processing

Made with ❤️ for a faster, cleaner download experience.
