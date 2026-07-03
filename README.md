# Subpar Nautica — An Ebonrift Survey

A complete first-person underwater exploration game in a **single `index.html`** file. Original story, creatures, and world — built with Three.js, procedural assets only (no downloads, no build step).

## How to run

1. Open a terminal in this folder.
2. Run `python -m http.server 8000`.
3. Open <http://localhost:8000/> in Google Chrome (internet is required to fetch Three.js from the CDN).
4. Click **“CLICK TO BEGIN”** and dive.

Do not open `index.html` through a `file://` URL. ES modules and embedded previews
treat local files as separate security origins, so browsers may refuse to load the
page or its dependencies.

A full playthrough of the golden path takes about 3–4 minutes.

## 分享給朋友遊玩

遊戲本體只有 `index.html`，因此可以直接把這個檔案分享給朋友。不過遊戲會從 CDN
載入 Three.js，所以遊玩時需要網路連線，而且不能直接雙擊 HTML 檔案開啟。

朋友可以將 `index.html` 放進一個資料夾，然後在該資料夾開啟終端機並執行：

```powershell
python -m http.server 8000
```

接著使用瀏覽器開啟 <http://localhost:8000/> 即可遊玩。電腦需要先安裝
[Python](https://www.python.org/downloads/)。

若希望朋友不必安裝 Python，建議將專案部署至 GitHub Pages、Netlify 或
Cloudflare Pages。部署後只需分享遊戲網址，朋友便能直接在瀏覽器中遊玩。

## Controls

| Input | Action |
|---|---|
| Mouse | Look / steer |
| W A S D | Swim / drive |
| Space / Ctrl | Ascend / descend |
| Shift | Jet-dash burst |
| E (hold) | Scan / interact |
| 1 2 3 | Quickbar — Scanner / Headlamp / Flare |
| Q | Throw flare |
| F | Enter / exit the sub |
| L | Sub headlights |
| V | Sub third-person camera |
| H | Hide HUD (Photo Mode) |
| F3 | Debug overlay |
| Esc | Pause — controls, quality, audio, databank |

## Quality settings

Default is **High** (bloom, god rays, full particles). If your machine struggles, open **Esc → QUALITY** and switch to **Medium** or **Low** — it applies instantly, no reload needed. Targets 60 FPS at 1080p on a mid-range GPU.
