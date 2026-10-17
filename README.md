<div align="center">

# 🎧 VibeDJ

### 🎶 Mix your tracks right in the browser! 🎶

A **two-deck DJ webapp** that runs entirely **locally** — no install, no server, no upload. 🔒
Load two tracks, let VibeDJ detect **BPM**, **beatgrid** and **harmonic key**, then **sync**, **EQ**, **filter**, add **effects**, isolate **stems**, set **loops** and **hot cues**, and **record** your set. 🚀

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Platform](https://img.shields.io/badge/platform-web%20browser-22d3ee.svg)
![PWA](https://img.shields.io/badge/PWA-installable-a78bfa.svg)
![Dependencies](https://img.shields.io/badge/dependencies-none-34d399.svg)
![Built with](https://img.shields.io/badge/built%20with-vanilla%20JS-f7df1e.svg)

[https://vibedj-one.vercel.app/](https://vibedj-one.vercel.app/)
</div>

---

## 📖 Table of contents

- [✨ Overview](#-overview)
- [🚀 Quick start](#-quick-start)
- [📁 Loading tracks](#-loading-tracks)
- [📚 Library & 🧠 track analysis](#-library--track-analysis)
- [🎛️ The decks](#️-the-decks)
- [🌊 Overlaid waveform & beatgrid](#-overlaid-waveform--beatgrid)
- [🔊 Effects](#-effects)
- [🎤 Stems](#-stems)
- [🎯 Loops & hot cues](#-loops--hot-cues)
- [🎚️ The mixer](#️-the-mixer)
- [🎙️ Recording](#️-recording)
- [⌨️ Keyboard shortcuts](#️-keyboard-shortcuts)
- [🔒 Privacy](#-privacy)
- [🛠️ Tech stack](#️-tech-stack)
- [🌐 Compatibility](#-compatibility)
- [📄 License](#-license)
- [👤 Author](#-author)

---

## ✨ Overview

🎧 **VibeDJ** gives you a classic two-channel DJ setup (deck **A** ▶️ + mixer 🎚️ + deck **B** ◀️) directly in the browser:

| 🎛️ | Feature |
| :---: | :--- |
| 🎵 | Two independent decks with full transport control |
| 🌀 | Scratch / scrub via a draggable jog wheel |
| ⚡ | One-tap **SYNC** (tempo + beat phase alignment) |
| 🌊 | Shared overlaid waveform with zoomable time axis |
| 🥁 | Automatic **beatgrid** with downbeats |
| 🧠 | **BPM**, **harmonic key (Camelot)** & **energy** detection |
| 🎚️ | 3-band EQ + kill, LP/HP filter, trim, faders, crossfader |
| 🔊 | Per-deck **delay**, **echo**, **flanger**, **reverb**, **phaser**, **bitcrush** |
| 🎤 | Per-deck **stems**: isolate vocal / instrumental / bass / drums |
| 🎯 | Beat loops (1/4 → 8) and **8 hot cues** per deck |
| 🥁 | **Quantize**, **beat jump** and **BPM/grid tools** |
| 🛡️ | Master **limiter** with a clip indicator |
| 📂 | Local **folder browser** with sorting, filtering & drag & drop |
| 🎙️ | **Record** the master output to a file |
| ⌨️ | Full **keyboard** control with on-screen tooltips |
| 📱 | Installable **PWA** (offline-capable) |

> 💡 Everything happens **in your browser**. VibeDJ never sends your music anywhere. 🔐

---

## 🚀 Quick start

1. 🌐 Open `index.html` in a modern browser (or serve the folder — see below).
2. 🎵 Drop two audio files onto the window (or use **LOAD TRACK**).
3. ▶️ Press **PLAY**, hit **SYNC** on the second deck, and start mixing! 🎚️
4. 🎙️ Press **RECORD** to capture your set, press it again to save the file.

**🖥️ Run locally (recommended for the Library & service worker):**

```bash
# any static server works 🚀
python -m http.server 8000
# then open http://localhost:8000/
```

> ⚠️ The **Library** folder picker and the **service worker** work best when served over `http(s)` — opening the file directly with `file://` limits some features.

---

## 📁 Loading tracks

You can load a track in several ways 🎯:

| 🖱️ Method | 📝 Description |
| :--- | :--- |
| 📥 **LOAD TRACK** button | Pick a file from your disk (deck A or B) |
| 🪂 **Drag & drop onto a deck** | Drop an audio file onto a specific deck |
| 🌍 **Drag & drop anywhere** | Drop **two** files → they land on **A** and **B** automatically (the *"Drop your tracks here"* overlay) |
| 📚 **Library modal** | Browse a folder and send a track to a deck |

Supported formats include **MP3, WAV, OGG, M4A, FLAC, AAC** (whatever your browser can decode 🎧).

Each deck shows the **file name**, **duration**, **mono/stereo** and **sample rate**. 📊

---

## 📚 Library & 🧠 track analysis

Open the **Library** with the top-bar **LIBRARY** button or the **F3** shortcut. 🗂️

- 📂 **SELECT FOLDER** — uses the modern **File System Access API** to browse a real folder, enter **subfolders** (double-click a `DIR` row, or `.. go up`) and **REFRESH**. 🔄
- 🗃️ In browsers without that API, it falls back to a **static list** from a folder input (works in Chrome/Edge). 🧩

Every audio row shows 🏷️:

| 🔎 | Column | Meaning |
| :---: | :--- | :--- |
| 📛 | **EXT tag** | File extension |
| 📄 | **NAME** | File name |
| 💾 | **SIZE** | File size (KB / MB) |
| ⏱️ | **TIME** | Duration |
| 🥁 | **BPM** | Estimated tempo |
| 🎼 | **KEY** | Harmonic key in **Camelot** notation (e.g. `1A`, `8B`) |
| ⚡ | **ENERGY** | Loudness tag `1`–`5` |

- 🟡 **Loaded tracks** are highlighted in **amber**.
- 🖱️ **Double-click** → loads the first **free** deck (or the one not playing).
- 🅰️🅱️ **A / B** buttons → send the track to a chosen deck.
- 🪂 **Drag a row** → drop it onto a deck.
- ⏳ Analysis (BPM/key/energy) runs **in the background** in a **Web Worker**, so the UI never freezes. 🧵
- 🔃 **Sort** by clicking a column header (name / size / time / BPM / key / energy) — click again to flip the order.
- 🔎 **Filter** the list with the search box above the columns. 🧲

**🧠 How the analysis works:**

- 🥁 **BPM + beatgrid** — an onset envelope is autocorrelated to find the tempo (≈70–180 BPM with octave correction and fractional refinement), then the beat phase is locked with a linear regression to build the **beatgrid**.
- 🎼 **Key** — a chromagram (Goertzel-style resonator bank) is matched against **Krumhansl–Schmuckler** major/minor profiles and mapped to **Camelot** notation.
- ⚡ **Energy** — derived from the coarse **RMS level** and quantized to a 1–5 scale.
- 🌈 **Waveform peaks** — the audio is split into **low / mid / high** bands for the colored overview.

---

## 🎛️ The decks

Each deck (A ▶️ blue / B ◀️ pink) is a full player. 💿

### 🕹️ Jog wheel
- 🌀 **Drag while playing** → scratch like vinyl (with inertia/momentum).
- ✋ **Drag while paused** → scrub through the track.
- 💡 Shows the deck letter, a **beat-flash ring** and a scratch ring while scratching.

### 🚦 Transport
| 🎛️ Control | 🎬 Action |
| :--- | :--- |
| ⏮️ **START** | Jump back to the beginning |
| ▶️ **PLAY / ⏸️ PAUSE** | Start / stop playback |
| 🔴 **CUE** | Set the cue point; **hold** to preview from cue; press to snap back |
| ⚡ **SYNC** | Match the other deck's tempo **and** beat phase |
| 🎚️ **TEMPO** fader | Change the tempo ±16% (also changes pitch — **no key lock**) |

### ⏭️ Beat jump & 🎚️ BPM/grid tools
- ⏭️ **Beat jump** — buttons `−4 · −2 · −1 · +1 · +2 · +4` jump whole beats (uses the detected BPM, defaults to 120 if none).
- 🎚️ **Grid tools** — `÷2` / `×2` halve or double the BPM (recalculated from the first downbeat), `◀` / `▶` nudge the grid, **SET** lets you type a BPM (40–240), and **TAP** tap-tempo from the beat.
- ⌨️ Every button in both rows has a **keyboard shortcut** — hover it or check the [shortcuts table](#️-keyboard-shortcuts).

### 📟 Deck readouts (above the jog)
`⏱️ total` · `⌛ left` (turns **amber** under 30 s) · `🥁 BPM` · `🎼 key`

The deck header also shows the **effective BPM** (base BPM adjusted by the tempo fader) and a **BPM badge**. 🏷️

---

## 🌊 Overlaid waveform & beatgrid

The top **`syncWave`** strip overlays **both decks in one shared time axis** 🌊 — deck **A on top**, deck **B on the bottom** — so you can truly compare the two tracks. 👀

- 🔍 **Zoom**: mouse **wheel**, the **−** / **+** buttons, or the **`[` / `]`** shortcuts → both decks zoom together.
- 🖱️ **Click to seek**: clicking the **top half** seeks deck **A**, the **bottom half** seeks deck **B**.
- 🎨 Each half renders a **3-band colored waveform** (low / mid / high).
- 🥁 **Beatgrid**: the grid of the deck you're listening to is **solid**, the other deck's is **dashed**; the marked bar is the **downbeat** (every 4 bars).
- 📏 Each half displays the **phase offset in ms** against the beat — nudge the **TEMPO** fader until both grids stay locked. 🔒
- 🧭 A small **graphical phase meter** compares both decks' phase (it turns the deck color when the beats are aligned). 🎯

Each deck additionally has its own **overview waveform** canvas you can click to seek. 📊

---

## 🔊 Effects

Each deck has its own chain of effects, toggled from the **FX row** (they stack in series): 🎛️

| 🎚️ Effect | 🧪 Character |
| :--- | :--- |
| **DELAY** | Short slap-back delay (≈0.28 s, moderate feedback) |
| **ECHO** | Longer repeats (≈0.42 s, strong feedback) |
| **FLANGER** | Modulated short delay with an LFO sweep 🌀 |
| **REVERB** | Convolution reverb with a generated impulse response 🌫️ |
| **PHASER** | 4-stage all-pass filter chain swept by an LFO (notch sweep, distinct from the flanger) 🎛️ |
| **BITCRUSH** | Lo-Fi bit-depth reduction (wave-shaper) with a downsample-emulating low-pass 🔻 |

Each effect crossfades **dry/wet** smoothly when toggled. ❇️ Effects chain as: `delay → echo → flanger → reverb → phaser → bitcrush`. 🔗

---

## 🎤 Stems

Each deck can **isolate a component of the mix** from the **STEMS row** (between the FX and bend rows). 🎚️ The four stems are **independent toggles**: switch one — or several — on to hear only the isolated component(s), and switch them all off to return to the **full mix**. 🔀

| 🎚️ Stem | 🧪 Isolation |
| :--- | :--- |
| **VOCAL** | Band-pass ≈ 380 Hz – 3.6 kHz (acapella-ish upper-mid) 🎙️ |
| **INST** | Full mix with a ≈ −18 dB notch at 1.2 kHz (vocals reduced → instrumental) 🎹 |
| **BASS** | Low-pass ≈ 220 Hz (bass only) 🔉 |
| **DRUMS** | High-pass ≈ 3 kHz (hats / cymbals and percussion top) 🥁 |

The stems are applied **after** the effects chain (`… → phaser → bitcrush → stems → channel`). 🔗 Each button is **colour-coded like rekordbox** — 🟣 vocal, 🟢 instrumental, 🔵 bass, 🟠 drums.

> ⚠️ These stems are a **filter-based approximation**, not machine-learning source separation: they shape the spectrum (and reduce centered vocals) rather than truly unmixing the track.

---

## 🎯 Loops & hot cues

### 🔁 Beat loops
- 🎚️ Quick presets: **1/4 · 1/2 · 1 · 2 · 4 · 8** beats (auto-sized from the detected BPM).
- ✂️ Manual **IN / OUT / EXIT** for free loop points.
- 🟢 The active loop highlights and playback wraps seamlessly. 🔄

> 🎯 Turn on **QUANTIZE** (top bar) to snap cue points, loops and hot cues to the nearest beat. ✨

### 🎨 Hot cues
- 🔢 **8 hot cues** per deck, each with its own **color**.
- ➕ Press an empty pad → **set** the cue.
- 🔁 Press a set pad → **jump** to the cue (with a glowing pad).
- 🧹 **Shift + click** → **clear** the cue.

---

## 🎚️ The mixer

The central mixer is a classic 2-channel strip. 🎛️

| 🎚️ Section | ✨ Details |
| :--- | :--- |
| **TRIM** 🎚️ | Input gain, −20 dB … +6 dB |
| **HI / MID / LOW** | 3-band EQ (high-shelf 6.5 kHz, peak 1.1 kHz, low-shelf 140 Hz) |
| **Kill** 🔇 | Per-band **K** buttons mute a band (−60 dB) |
| **FILTER** 🌊 | Bipolar **LP / HP** filter (low-pass down to ~200 Hz, high-pass up to ~2 kHz) |
| **Channel faders** 📉 | Smooth `gain^1.6` curve per channel |
| **CROSSFADER** ↔️ | **Constant-power** curve (cosine/sine) between A and B |
| **MASTER** 🔊 | Master output level |
| **Limiter** 🛡️ | Master limiter before the output/recording with a **clip LED** that flashes on overload |
| **PHONES** 🎧 | Headphone / cue-bus level |
| **Meters** 📊 | Per-channel + stereo master meters with **peak hold** |
| **PFL** 🎧 | Exclusive headphone monitoring of one deck (pre-fader) |

---

## 🎙️ Recording

- 🔴 Hit **RECORD** to start capturing the **master output** (a `MediaRecorder` taps the master bus).
- ⏱️ A live **timer** shows the elapsed time.
- ⏹️ Press **RECORD** again to **stop** → the mix is downloaded automatically as `mix_YYYYMMDD_HHMMSS.webm` 📥 (or `.ogg` / `.m4a`, depending on the best codec your browser supports). 🎧

---

## ⌨️ Keyboard shortcuts

VibeDJ is fully playable from the keyboard. ⌨️🎉

- 🪞 **Mirrored layout**: deck **A** uses the **left** half of the keyboard, deck **B** mirrors it on the **right**.
- 💬 Every control shows its key in its **tooltip** — just hover it. 🖱️
- 🎚️ **Analog controls**: press the control's key to **select** it, then use **↑ / ↓** to adjust.
- 🔠 Shortcuts are **case-sensitive** (e.g. `z` vs `Shift+Z` are different cues).
- 🎤 The **stems** use the **Alt** modifier (`Alt+1..4` on A, `Alt+7..0` on B), mirroring the effects layout.

### 🎛️ Deck shortcuts

| 🎬 Action | Deck A | Deck B |
| :--- | :---: | :---: |
| 📥 Load track | `\` | `'` |
| ❌ Eject | `1` | `ì` |
| ⏮️ Start | `A` | `H` |
| ▶️ Play / Pause | `S` | `J` |
| 🔴 Cue (hold) | `D` | `K` |
| ⚡ Sync | `F` | `L` |
| 🎯 Hot cues 1–4 | `Z X C V` | `/ . , m` |
| 🎯 Hot cues 5–8 | `Shift+Z X C V` | `Shift+/ . , m` |
| 🔁 Loop in / out / exit | `Q W E` | `I O P` |
| 🔢 Loop 1/4 · 1/2 · 1 · 2 · 4 · 8 | `Shift+5 ~ 2 3 4 5` | `Shift+6 \| 6 7 8 9` |
| ↘️↗️ Bend − / + (hold) | `-` / `+` | `.` / `è` |
| 🔊 Effects: delay / echo / flanger / reverb / phaser / bitcrush | `Shift+1..4` · `Shift+B` · `Backtick` | `Shift+7..0` · `Shift+N` · `=` |
| 🎤 Stems: vocal / instrumental / bass / drums | `Alt+1..4` | `Alt+7..0` |
| ⏭️ Beat jump −4 · −2 · −1 · +1 · +2 · +4 | `Shift+Q W E R T Y` | `Shift+U I O P { }` |
| 🎚️ Grid ÷2 · ×2 · nudge ◀ · ▶ · SET · TAP | `Shift+A S D F G H` | `Shift+J K L ; : "` |
| 🔇 Kill highs / mids / lows | `T G B` | `Y H N` |
| 🎚️ Pitch | `PageUp` | `PageDown` |
| 📉 Volume | `Insert` | `Delete` |
| 🎼 Highs / Mids / Lows | `F7 F9 F11` | `F8 F10 F12` |
| 🌊 Filter | `Home` | `End` |

### 🎚️ Mixer & 🌍 global shortcuts

| 🎬 Action | Key |
| :--- | :---: |
| 🔴 Record | `F6` |
| 🎯 Quantize on / off | `F1` |
| 🔊 Master | `F4` |
| 🎧 Phones | `F5` |
| ↔️ Crossfader | `←` / `→` |
| 📚 Library | `F3` |
| ❓ Shortcuts / Help | `F2` |
| 🔍 Zoom in / out | `]` / `[` |
| 🎯 Select control | `↑` / `↓` |
| ❌ Close modal / deselect | `Esc` |

> 🛠️ The whole keymap lives in a single **`SHORTCUT_CONFIG`** object in `index.html` — swap any key to build your own layout. ✏️
> ℹ️ Some slots (like **PFL** and **Trim**) may be left unassigned in the current layout.
> ♿ Knobs and faders are **keyboard-focusable** (Tab) and respond to **↑ / ↓ / Home / End**; every slider exposes its value to screen readers.

---

## 🔒 Privacy

- 🏠 **100% local** — audio is decoded and played in your browser.
- 🚫 **Nothing is uploaded** — there is no backend, no account, no tracking.
- 💾 Your files never leave your machine. 🛡️

---

## 🛠️ Tech stack

| 🧩 | Technology |
| :---: | :--- |
| 🎨 | **HTML5 + CSS** (dark neon UI, Canvas rendering) |
| 🟨 | **Vanilla JavaScript** — zero dependencies, no build step |
| 🔊 | **Web Audio API** (Graph of gains, biquads, delays, convolver) |
| 🧵 | **Web Workers** for BPM/beat analysis off the main thread |
| 📂 | **File System Access API** (+ folder-input fallback) for the Library |
| 🎙️ | **MediaRecorder** for capturing the mix |
| 📱 | **PWA** — `manifest.json` + service worker for offline use |

**🗂️ Project files**

```
📦 VibeDJ
 ┣ 📜 index.html      → the whole app (UI + audio engine + analysis)
 ┣ 📜 sw.js           → service worker (offline cache)
 ┣ 📜 manifest.json   → PWA manifest
 ┗ 🖼️ favicon.ico     → app icon
```

---

## 🌐 Compatibility

- ✅ Best in **Chrome / Edge** (File System Access API, MediaRecorder codecs).
- ✅ Works in **Firefox / Safari** with the Library's static-list fallback.
- 🎧 A **headset** is recommended to use **PFL** headphone monitoring.

---

## 📜 License

Distributed under the **MIT License**. Feel free to use, modify, and share.

---

> 🌱 *Made with ❤️ and 🧠. If you find this tool helpful, please leave a ⭐ on GitHub!*
