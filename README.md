<div align="center">

# 🎧 VibeDJ

### 🎶 Mix your tracks right in the browser! 🎶

A **two-deck DJ webapp** that runs entirely **locally** — no install, no server, no upload. 🔒
Load two tracks, let VibeDJ detect **BPM**, **beatgrid** and **harmonic key**, then **sync**, **EQ**, **filter**, add **effects**, mute/unmute **stems**, set **loops** and **hot cues**, and **record** your set. 🚀

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
- [🖥️ Interface, modals & UI zoom](#️-interface-modals--ui-zoom)
- [📁 Loading tracks](#-loading-tracks)
- [📚 Library & 🧠 track analysis](#-library--track-analysis)
- [🎛️ The decks](#️-the-decks)
- [🌊 Overlaid waveform & beatgrid](#-overlaid-waveform--beatgrid)
- [🔊 Effects](#-effects)
- [🎤 Stems](#-stems)
- [🎯 Loops & hot cues](#-loops--hot-cues)
- [🎚️ The mixer](#️-the-mixer)
- [🎙️ Recording](#️-recording)
- [🎛️ MIDI controller & DDJ-FLX4](#️-midi-controller--ddj-flx4)
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
| ⚡ | One-tap **SYNC** (tempo + beat phase alignment, tempo range widened to ±16% when needed) |
| 🌊 | Shared overlaid waveform with zoomable time axis, coloured by frequency band and following the stem mutes |
| 🥁 | Automatic **beatgrid** with downbeats |
| 🧠 | **BPM**, **harmonic key (Camelot)** & **energy** detection |
| 🎚️ | 3-band EQ + kill, LP/HP filter, trim, faders, crossfader |
| 🔊 | Per-deck **delay**, **echo**, **flanger**, **reverb**, **phaser**, **bitcrush** |
| 🎤 | Per-deck **stems** (rekordbox-style): mute / unmute vocal, instrumental, bass and drums |
| 🎯 | Beat loops (1/4 → 8) and **8 hot cues** per deck |
| 🥁 | **Quantize**, **beat jump** and **BPM/grid tools** |
| 🛡️ | Master **limiter** with a clip indicator |
| 📂 | Local **folder browser** with sorting, filtering & drag & drop |
| 🎙️ | **Record** the master output to a file |
| 🎛️ | **MIDI controller** support (Pioneer **DDJ-FLX4** map): full bidirectional MIDI mapping, LEDs, an editable map and master audio routing |
| 🥁 | **Beat LEDs** for both decks in the mixer header |
| ⌨️ | Full **keyboard** control with on-screen tooltips and an in-app **key-map editor** |
| 🔍 | **UI zoom** — `−` / `+` buttons in the top bar resize the whole interface (30% → 120%, 10% steps) with a live **% readout**: every element scales uniformly, waveform strip included, so nothing is cut off; when zoomed out the decks and mixer shrink while the waveform strip stretches vertically to fill all the remaining page space, leaving no empty gap at the bottom (modals, toasts and tooltips zoom too) and the level is **remembered** between sessions |
| 💾 | **Remembered settings** — UI zoom, key map, MIDI map and audio output survive a reload |
| 📱 | Installable **PWA** (offline-capable) |

> 💡 Everything happens **in your browser**. VibeDJ never sends your music anywhere. 🔐

---

## 🚀 Quick start

1. 🌐 Open `index.html` in a modern browser (or serve the folder — see below).
2. 🎵 Drop two audio files onto the window (or use **LOAD TRACK**).
3. ▶️ Press **PLAY**, hit **SYNC** on the second deck, and start mixing! 🎚️
4. 🎙️ Press **RECORD** to capture your set, press it again to save the file.
5. 🎛️ Optional: press **MIDI** to connect a **DDJ-FLX4**, **HELP** (`F2`) for the shortcut table and the key-map editor, **ABOUT** for the credits.
6. 🔍 Use the **− / % / +** controls in the centre of the top bar to zoom the interface.

**🖥️ Run locally (recommended for the Library & service worker):**

```bash
# any static server works 🚀
python -m http.server 8000
# then open http://localhost:8000/
```

> ⚠️ The **Library** folder picker and the **service worker** work best when served over `http(s)` — opening the file directly with `file://` limits some features.

---

## 🖥️ Interface, modals & UI zoom

The top bar is **sticky** and always reachable. 🧭

| 🎛️ Area | ✨ What it does |
| :--- | :--- |
| 🎧 **Brand** | App name plus the tagline |
| 🔍 **Zoom cluster** (centre) | `−` / **% readout** / `+` for the **interface zoom** (30% → 120%, 10% steps); the buttons grey out at the limits |
| 🔴 **RECORD** | Starts / stops the mix capture, with the elapsed timer next to it |
| 📚 **LIBRARY** (`F3`) | Opens the local folder browser |
| 🎛️ **MIDI** | Connects / disconnects the MIDI controller and opens its dialog |
| ❓ **HELP** (`F2`) | Opens **How to use**: feature list, shortcut table and key-map editor |
| ℹ️ **ABOUT** | Credits, synopsis and repository links |

**🔍 UI zoom** applies a single CSS `zoom` to the whole app: decks, mixer, waveform strip, **modals, toasts and tooltips** scale together, so nothing is clipped. The canvases are re-measured and repainted at their new pixel size after every step — in or out — so the shared strip and the deck overviews keep their full waveform at any level. When the effective width or height gets small the layout reflows (the decks stack vertically and the jog wheels shrink). The percentage shown in the top bar is stored in `localStorage` and restored at the next start. It is **independent** of the beat-locked waveform zoom described [below](#-overlaid-waveform--beatgrid).

**🪟 Modals** (Library, Help, MIDI, About) close with their **CLOSE** button, a click on the dark backdrop or `Esc`; focus moves inside the dialog and `Tab` cycles only through its controls. Pressing `Esc` with no modal open drops the analog control currently bound to the arrow keys.

**💬 Tooltips and toasts** — every control exposes a tooltip (and, when it has one, its **keyboard shortcut**); the bubble flips above or below the element to stay on screen. Short feedback (track loaded, BPM found, mode toggled…) appears as a toast at the bottom of the window for a few seconds.

**♿ Accessibility** — knobs and faders are focusable (`Tab`) with `role="slider"` and live values for screen readers; the control selected from the keyboard gets an amber outline.

---

## 📁 Loading tracks

You can load a track in several ways 🎯:

| 🖱️ Method | 📝 Description |
| :--- | :--- |
| 📥 **LOAD TRACK** button | Pick a file from your disk for that deck |
| 🪂 **Drag & drop onto a deck** | Drop files onto a specific deck: the first stays there, a second one goes to the other deck |
| 🌍 **Drag & drop anywhere** | Drop files anywhere in the window (the *"Drop your tracks here"* overlay pops up): they fill the **free** decks first (**A**, then **B**); with both decks loaded the first file goes to deck **A** |
| 📚 **Library modal** | Browse a folder and send a track to a deck |

Supported formats include **MP3, WAV, OGG, M4A, FLAC, AAC** (whatever your browser can decode 🎧); anything else is rejected with a toast. 🚫

- 🛡️ A deck **refuses** to load while it is **playing** or still **decoding** another file — a toast explains why.
- ❌ **EJECT** (the `✕` button in the deck header) unloads the track and clears its cue point, loops, hot cues and analysis.
- ⏳ Progress arrives as toasts — *decoding…* → *loaded — analyzing BPM…* → *`124.0 BPM · beatgrid ready`* (or *BPM not detected*). Tracks shorter than **8 s** get no beatgrid, and key detection needs at least **2 s** of audio.

Each deck shows the **file name** with its **mono/stereo** and **sample rate** — nothing more: the times (`⏱️ total` and `⌛ left`) live in the jog readout above, so the line under the name stays still while playing. 📊

---

## 📚 Library & 🧠 track analysis

Open the **Library** with the top-bar **LIBRARY** button or the **F3** shortcut. 🗂️

- 📂 **SELECT FOLDER** — uses the modern **File System Access API** to browse a real folder and **REFRESH** it. 🔄 The list shows **only the playable audio files that sit directly in the selected folder**: subfolders are never listed and their content is not scanned.
- 🗃️ In browsers without that API, it falls back to a **static list** from a folder input (works in Chrome/Edge). 🧩 Same rule: only the files directly inside the picked folder are listed.
- 🧭 The chosen folder is shown next to **BROWSE · Local folder:** (tagged *(static list)* in fallback mode); hidden dot-files and non-audio files are skipped.

Every audio row shows 🏷️:

| 🔎 | Column | Meaning |
| :---: | :--- | :--- |
| 📛 | **FORMAT** | File extension (uppercased, 4 characters max) |
| 📄 | **NAME** | File name |
| 💾 | **SIZE** | File size (KB / MB) |
| ⏱️ | **TIME** | Duration |
| 🥁 | **BPM** | Estimated tempo |
| 🎼 | **KEY** | Harmonic key in **Camelot** notation (e.g. `1A`, `8B`) |
| ⚡ | **ENERGY** | Loudness tag `1`–`5` |

- 🟡 **Loaded tracks** are highlighted in **amber**.
- 🎛️ With a MIDI controller connected, the row selected with the **BROWSE** rotary is highlighted in **cyan** — the highlight is only drawn while the controller is active.
- 🖱️ **Double-click** → loads the first **free** deck (or the one not playing).
- 🅰️🅱️ **A / B** buttons → send the track to a chosen deck. The button stays lit in that deck's colour while the track is loaded there (and blinks while it is playing), so you always see where each track currently sits.
- 🪂 **Drag a row** → drop it onto a deck.
- ⏳ Analysis (BPM/key/energy) runs **in the background** in a **Web Worker**, so the UI never freezes. 🧵 Cells stay at `--` until their file has been decoded and analysed (files are processed **one at a time**), and a file that cannot be decoded is **dropped from the list**.
- 🔃 **Sort** by clicking a column header (name / size / time / BPM / key / energy) — click again to flip the order; the active column shows a **▲ / ▼** arrow.
- 🔎 **Filter** the list with the search box above the columns. 🧲

**🧠 How the analysis works:**

- 🥁 **BPM + beatgrid** — an onset envelope is autocorrelated to find the tempo (≈70–180 BPM with octave correction and fractional refinement), then the beat phase is locked with a linear regression to build the **beatgrid**.
- 🎼 **Key** — a chromagram (Goertzel-style resonator bank) is matched against **Krumhansl–Schmuckler** major/minor profiles and mapped to **Camelot** notation.
- ⚡ **Energy** — derived from the coarse **RMS level** and quantized to a 1–5 scale.
- 🌈 **Waveform peaks** — the audio is split into **low / mid / high** bands, used both for the shared waveform strip and for the colored deck overview.

---

## 🎛️ The decks

Each deck (A ▶️ blue / B ◀️ pink) is a full player. 💿

### 🕹️ Jog wheel
- 🌀 **Drag while playing** → scratch like vinyl (with inertia/momentum).
- ✋ **Drag while paused** → scrub through the track.
- 📍 The **rotating cursor** on the platter is **phase-locked to the beatgrid**: it turns once per **bar** (4 beats), so it points straight up at **12 o'clock on every downbeat** — exactly where the thick grid lines are — and slows down or speeds up with the tempo. A track whose beatgrid was not detected falls back to a fixed turn every 1.8 s.
- 💡 Shows the deck letter, a **beat-flash ring** and a scratch ring while scratching.

### 🚦 Transport
| 🎛️ Control | 🎬 Action |
| :--- | :--- |
| ⏮️ **START** | Jump back to the beginning |
| ▶️ **PLAY / ⏸️ PAUSE** | Start / stop playback (the label follows the state; while the deck is stopped the **PLAY** label is green, and it lights up the whole button only during playback) |
| 🔴 **CUE** | Set the cue point; **hold** to preview from cue; press to snap back; **right-click** to clear the stored cue point — the button shows its amber colour only while a cue is stored, standard grey otherwise; the CUE text blinks while paused away from the cue point, like a real console |
| ⚡ **SYNC** | Match the other deck's tempo **and** beat phase (both decks need a detected BPM). When the required pitch does not fit the current range the fader range **widens to ±16% on its own** (switch and cursor follow) and the match goes ahead; when even **±16%** is not enough the sync is **blocked** — the deck keeps its tempo, position and range — and a toast reports the pitch it would have needed |
| 🎚️ **TEMPO** fader | Change the tempo inside the selected range (also changes pitch — **no key lock**); oriented like the hardware, so sliding up slows down and sliding down speeds up |
| ↔️ **Range switch** (under the `TEMPO` label) | Shows the fader's current maximum travel (`±8%` / `±16%`): click it to jump between **±8%** (default, knob left) and **±16%** (knob right, highlighted); switching back to ±8% pulls any larger pitch into range and the tempo follows immediately. **SYNC** raises it to ±16% by itself when the other deck needs more than 8%, and refuses to sync when the target is beyond ±16% |
| ↘️↗️ **BEND − / +** | **Hold** for a temporary pitch bend (∓5%) that springs back to the fader value on release |
| ❌ **EJECT** | Unload the track (`✕` in the deck header) and clear its cue, loops and hot cues |

### ⏭️ Beat jump & 🎚️ BPM/grid tools
- ⏭️ **Beat jump** — buttons `−16 · −8 · −4 · +4 · +8 · +16` jump whole beats (uses the detected BPM, defaults to 120 if none). The jump always moves by **exactly N beats** and keeps the **phase inside the beat** the deck is playing at, so two decks whose downbeats are synced stay locked beat for beat; with **QUANTIZE** on the landing point is still snapped to the beatgrid, but *relative to that phase*, so the jump cleans up the position without ever shifting the beat alignment (the BPM was already matched and stays matched).
- 🎚️ **Grid tools** — `÷2` / `×2` halve or double the BPM (recalculated from the first downbeat), `◀` / `▶` nudge the grid by **1 ms** per click (the grid shifts rigidly, so its spacing and bar numbering stay intact at the track edges too, where beats that fall outside the track are simply not drawn), **SET** lets you type a BPM (40–240), and **TAP** tap-tempo averages up to the last **9** taps (the series restarts after a 2.5 s pause).
- ⌨️ Every button in both rows has a **keyboard shortcut** — hover it or check the [shortcuts table](#️-keyboard-shortcuts); triggering one from the keyboard or the controller **flashes the button**.

### 📟 Deck readouts (above the jog)
`⏱️ total` · `⌛ left` (turns **red and blinks** under 30 s) · `🥁 BPM` · `🎼 key`

The deck header carries the **BPM badge** (the track's base tempo); the **effective BPM** (base tempo adjusted by the tempo fader) is the `🥁 BPM` readout in the jog info above, so it is not repeated in the header. 🏷️

---

## 🌊 Overlaid waveform & beatgrid

The top **`syncWave`** strip overlays **both decks in one shared time axis** 🌊 — deck **A on top**, deck **B on the bottom** — so you can truly compare the two tracks. 👀

- 🔍 **Zoom**: mouse **wheel**, the **−** / **+** buttons, or the **`[` / `]`** shortcuts → both decks zoom together. The window is **beat-locked**: the same number of beats stays visible at any tempo (the default 8 s window holds 16 beats at 120 BPM), clamped between 0.5 s and the longest loaded track (never below 2 s).
- 🖱️ **Click to seek**: clicking the **top half** seeks deck **A**, the **bottom half** seeks deck **B**; **dragging** left or right scrubs that deck continuously.
- 🎨 Each half renders a **3-band waveform**, every band in its **own fixed colour** — 🔴 **lows `#FF3B3B`**, 🟢 **mids `#16A34A`**, 🔵 **highs `#2563EB`** — as **three filled contours stacked from the loudest band down to the quietest**: the weakest layer is drawn **last**, so it sits in the **foreground** and stays readable even when the bass or the treble is much louder than it. The layers are **semi-transparent** (≈45 %), so where two or three bands overlap the colours blend instead of covering each other and every component stays visible. The **stacking order is fixed for the whole track** — it is computed once over all the peaks (and again only when the track or the stem mutes change), never from the moving window — so no part of the waveform ever flips to another colour while it plays. The outer edge of every column always follows the loudest band, so the silhouette keeps its shape.
- 🪶 Each layer is a **single continuous contour** — the top and bottom edges are joined into one closed path per band and filled in one go, so the whole strip costs **three fills per deck** instead of thousands of bars, keeps its transients and stays perfectly smooth while it scrolls.
- 🧊 **Only what changed is redrawn**: the strip is skipped entirely when the playhead, the zoom, the size, the stem mutes or the markers have not moved (the check is a single 32-bit hash, no strings, so nothing is allocated per frame), so a paused interface costs no rendering at all and every other moving element keeps its framerate.
- 🧈 **Nothing heavy runs on the audio thread's tab**: canvas sizes are cached and refreshed by a `ResizeObserver` instead of being measured every frame (no forced layout inside the animation loop), the jog wheel's disc and grooves are rendered once per size and blitted, the level meters refresh at 30 Hz and the time / tempo / key labels at ~11 Hz — the frame body during playback stays around **1–2 ms** and allocates nothing.
- 🎤 The strip follows the **stem mutes** (see [Stems](#-stems)): muting a stem attenuates the bands it belongs to, so the contour shows what you actually hear. The per-deck overview above the jog wheel always keeps the full mix.
- 💫 **No shimmer while playing**: the envelope is built from the peaks once and then **sampled with linear interpolation** at every column centre, so the three contours are continuous functions of the playhead instead of being re-quantised for each frame, and the whole waveform simply slides with the track.
- 📊 **Track progress**: a thin strip along the top of each half shows the elapsed time over the whole track in the deck colour, with a bright cursor on the leading edge; it follows the real playback position (so it rewinds with a loop) and is display-only — seeking stays on the waveform below.
- 🥁 **Beatgrid**: the grid of the deck you're listening to is **solid**, the other deck's is **dashed**; the thick bar is the **downbeat**, every **4 beats** (one bar), and the active deck's grid prints its `bar.beat` number next to each line. The grid is built only from the beats that actually fall **inside the track**, so every line keeps the spacing of its BPM and the closing bars are never drawn as a phantom beat squeezed onto the end of the file. 🎯
- 🚩 A thin **red playhead** runs down the centre of each half, where the waveform scrolls past.
- 🎯 **Markers** — the active loop range is shaded in green with solid edges, the cue point is a white flag marked `C` and every stored hot cue is a coloured flag with its number, drawn on both the shared strip and the deck overview.
- 📏 Each half displays the **phase offset in ms** against the beat — nudge the **TEMPO** fader until both grids stay locked. 🔒
- 🧭 A small **graphical phase meter** compares both decks' phase (amber while they drift, deck colour once they are within ±8% of half a beat). 🎯

Each deck additionally has its own **overview waveform** canvas you can click (or drag) to seek. 📊 On long tracks the contour heights come from the **average** band energy (not the per-column peak) and every band keeps its **own colour and its own shape** (🔴 lows, 🟢 mids, 🔵 highs), stacked from the loudest down to the quietest so the weak components stay in front even when the whole track is squeezed into a few hundred pixels. The envelope is smoothed across neighbouring columns and drawn with generous headroom, so the overview keeps a readable shape and never clips to white. The contour is built symmetrically around its centre line and is repainted from the cached peaks whenever the canvas changes size, so **both halves stay complete at every interface zoom level**, enlarging or shrinking.

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

The **STEMS row** (between the FX and bend rows) works like rekordbox's **ACTIVE STEM** controls: 🎚️ all four parts — **VOCAL**, **INST**, **BASS**, **DRUMS** — play by default (full mix) and each button **mutes / unmutes its own part**, so you can cut just the vocals, just the bass, and so on. 🔀 Mute them all and the deck goes silent.

| 🎚️ Stem | 🧪 When the stem is muted the… |
| :--- | :--- |
| **VOCAL** | …the **centre** of the mix (mid = (L+R)/2) inside the **180 Hz – 4 kHz** band is removed through a **centre-dominance** mask — the mid/side ratio of the band is measured over ~16 ms, then **sharpened (γ = 1.5), over-subtracted (× 1.35) and held for 150 ms** so the gaps between syllables stay closed, while **short transients inside the band itself** (snare, clap, kick body) re-open it so percussion keeps its punch — plus a **mute notch** that follows the same mask and pulls down what the *other* stems still hold in the vocal region: **97 %** of the residual mid, **70 %** of the side (the stereo reverb and doubling around a voice) and **95 %** of the centre treble, so the sibilants and presence go with the voice instead of staying in INST 🎙️ |
| **INST** | …the rest is removed: side content, non-centred mid and the band above 4 kHz, minus drum transients 🎹 |
| **BASS** | …the band below **180 Hz** is removed, except for drum attacks (the kick transient belongs to DRUMS), and while BASS is muted the drums' low end is cut by a further **90 %**, so the mute really empties the bottom instead of leaving the kick body behind 🔉 |
| **DRUMS** | …drum transients are removed: the kick attack from the low band plus snare / hats / cymbals from the mid-high bands, caught by a **more sensitive treble detector** (threshold 1.30, expanded, 8 ms release), leaving the kick body and sustain in BASS 🥁 |

The stems are applied **after** the effects chain (`… → phaser → bitcrush → stems → channel`). 🔗 Buttons are **colour-coded** — 🟢 vocal `#16A34A`, 🔵 instrumental `#2563EB`, 🔴 bass `#DC2626`, 🟠 drums `#EA580C` — and their background fills **only while the part is muted** (the mute is engaged); an audible part keeps the neutral button background. 🎛️

**🔁 Waveform feedback.** The shared **`syncWave`** strip redraws from what is still audible: each muted stem attenuates the bands it owns, so cutting the bass removes the low-frequency body of the contour while the kick transients survive in DRUMS, and cutting the drums flattens the transients and the air. The weights are a **frequency approximation** of the stem split, not the DSP gains:

| 🎚️ Stem muted (others on) | 🔉 Lows | 🎼 Mids | 🎼 Highs |
| :--- | :---: | :---: | :---: |
| **VOCAL** | 1.00 | 0.50 | 1.00 |
| **INST** | 1.00 | 0.68 | 0.55 |
| **BASS** | 0.12 | 1.00 | 1.00 |
| **DRUMS** | 0.88 | 0.82 | 0.45 |

🎨 The waveform uses the same three bands the filters work on, each in its **own colour and its own layer**: 🔴 **lows `#FF3B3B`**, 🟢 **mids `#16A34A`**, 🔵 **highs `#2563EB`**, the weakest of the three always in front and all of them **semi-transparent** so overlaps show every component at once. Muting a stem attenuates the bands it owns, so the layer it holds literally shrinks — cut the bass and the red body of the contour collapses while the green mids and the blue air stay, cut the drums and the blue transients flatten. The strip and the per-deck overview share the same layers, so the region you are about to cut is easy to find in both. 🎯

With all four stems on, the strip shows the full mix exactly as before. The per-deck overview above the jog wheel stays on the full mix, so the two views answer different questions: "what does the track look like" and "what am I hearing right now". 👀

> ⚠️ These stems are a **frequency + transient approximation**, not machine-learning source separation. The signal is split into three bands with **8th-order Linkwitz-Riley** crossovers at **180 Hz** and **4 kHz** — steeper than the previous 4th order, so a single mute leaks ~**24 dB less** of the other stems' share around the crossover — and the four stems are derived with time-varying gains (centre-dominance for VOCAL, fast/slow envelope transient masks for DRUMS, kick attack vs bass sustain) that **sum back to the dry signal** — no inverted-cancellation comb filtering. The **mute notches** above are the only part outside that partition and they engage only while a stem is muted. The gains run at audio rate in an **AudioWorklet** (zero added latency, no model downloads, ~3.7 % of a core per deck while a stem is muted), with the old biquad chain kept only as a fallback. ⚡ With all four parts audible the worklet does **no filtering at all**: the stems add back up to the dry signal, so the input is copied straight through (≈**0,3 %** of a core per deck) — the switch is crossfaded over ~12 ms and the filter states are reset while the output is still fully dry, so pressing the first mute never clicks. With all stems on the deck is transparent (**−0.01 dB**). Measured on a busy mix (centred voice with sibilance and reverb + wide pad + kick / snare / hats + bass): **VOCAL off** drops **440–1760 Hz by −23 dB**, the 220 Hz harmonic by −13 dB and the 6.5 kHz sibilance by −9 dB (previously −15 dB, −7 dB and −1 dB), while the wide pad loses 7.5 dB and the bass stays at 0 dB; **INST off** on a pure instrumental takes a wide pad down −10 dB, a centred lead −6 dB and 8 kHz air −64 dB; **BASS off** pushes a 90 Hz tone and the kick body to **−48 dB** (previously −25 / −28 dB); **DRUMS off** removes the kick attack (0–16 ms) by **−15 dB** while the sustain (60–100 ms) stays within 1 dB. On a **mono** track there is no centre to extract, so VOCAL mute is a no-op (INST/BASS/DRUMS still work); content below 180 Hz never belongs to VOCAL, so a deep male fundamental stays in BASS.

---

## 🎯 Loops & hot cues

### 🔁 Beat loops
- 🎚️ Quick presets: **1/4 · 1/2 · 1 · 2 · 4 · 8** beats (auto-sized from the detected BPM; they stay **disabled** until a tempo is known).
- ✂️ Manual **IN / OUT / EXIT** for free loop points.
- 🟢 The active loop highlights and playback wraps seamlessly. 🔄
- 📌 Changing the loop length of an **existing** loop (preset buttons, FLX4 pads or knob) keeps the original **IN** point and only moves the **OUT** — the loop grows or shrinks around its own start instead of jumping to the current position.
- ⏳ While the loop is **playing** the new width is **armed, not immediate**: the pass in progress runs to the OUT it had when you pressed — shorter *or* longer — and the following pass starts with the new width. The playhead is never yanked back to IN in the middle of a cycle, and nothing restarts mid-audio. Only when the deck is paused does the new length apply at once.
- 🛡️ **OUT** needs a valid **IN** first and a position after it, otherwise a toast tells you what is missing.

> 🎯 **QUANTIZE** (switch next to the PHONES knob in the mixer) is **on by default** and snaps cue points, loops and hot cues to the nearest beat, while beat jumps land on the grid without changing the phase they started from; switch it off when you want the raw positions. ✨

### 🎨 Hot cues
- 🔢 **8 hot cues** per deck, each with its own **color**.
- ➕ Press an empty pad → **set** the cue.
- 🔁 Press a set pad → **jump** to the cue (with a glowing pad).
- 🧹 **Shift + click** (or **right-click** on a pad) → **clear** the cue.

---

## 🎚️ The mixer

The central mixer is a classic 2-channel strip. 🎛️

| 🎚️ Section | ✨ Details |
| :--- | :--- |
| **TRIM** 🎚️ | Input gain, −20 dB … +6 dB |
| **HI / MID / LOW** | 3-band EQ (high-shelf 6.5 kHz, peak 1.1 kHz, low-shelf 140 Hz), −26 dB … +12 dB |
| **Kill** 🔇 | Per-band **K** buttons mute a band (−60 dB) |
| **FILTER** 🌊 | Bipolar **LP / HP** filter (low-pass down to ~200 Hz, high-pass up to ~2 kHz); LP values of 1 kHz or more are shown compactly, e.g. `18.2k` |
| **Channel faders** 📉 | Smooth `gain^1.6` curve per channel |
| **CROSSFADER** ↔️ | **Constant-power** curve (cosine/sine) between A and B |
| **MASTER** 🔊 | Master output level (`gain^1.5`, **50% by default**) |
| **Limiter** 🛡️ | Master limiter before the output/recording with a **clip LED** that stays lit for 1.5 s after an overload |
| **PHONES** 🎧 | Headphone / cue-bus level (**50% by default**) |
| **Meters** 📊 | 14-segment per-channel + stereo master meters with **peak hold** |
| **Beat LEDs** 🥁 | Two rows of 4 LEDs in the mixer header follow the beat position (1–4) of deck **A** and **B** in each deck's colour, with the first LED of the bar brighter |
| **PFL** 🎧 | Exclusive headphone monitoring of one deck (pre-fader) |
| **QUANTIZE** 🎯 | Toggle switch next to the PHONES knob, **on by default**: snaps cue points, hot cues, loops and beat jumps to the beatgrid |

🎛️ **Knob & fader gestures** — drag a knob **vertically** (hold **Shift** for fine steps) and **double-click** it to snap back to its default (trim / EQ / filter centred, master 50%, phones 50%); faders follow the pointer. Every knob and fader is keyboard-focusable and responds to `↑` / `↓` / `Home` / `End`.

---

## 🎙️ Recording

- 🔴 Hit **RECORD** to start capturing the **master output** (a `MediaRecorder` taps the master bus).
- ⏱️ A live **timer** shows the elapsed time.
- ⏹️ Press **RECORD** again to **stop** → the mix is downloaded automatically as `mix_YYYYMMDD_HHMMSS.webm` 📥 (or `.ogg` / `.m4a`, depending on the best codec your browser supports). 🎧

---

## 🎛️ MIDI controller & DDJ-FLX4

Press **MIDI** in the top bar to connect a **Pioneer DDJ-FLX4** over USB (Web MIDI, Chrome / Edge): the button lights up while the controller is bound and the same press opens the **MIDI controller** dialog. The full surface is mapped and **bidirectional**: moving a control updates the interface, and the interface (including keyboard shortcuts and preset loops) lights up the controller LEDs. Press **MIDI** again to disconnect — the edited map is kept.

- 🔍 **Detection** — any MIDI port whose name contains `DDJ-FLX4` or `FLX4` is picked up automatically. Close rekordbox and any other app holding the controller's MIDI port before connecting. 🚫
- 📊 **Status line** — the dialog reports *not connected* / *waiting for a controller* / *connected · MIDI in/out ready · audio: …*.
- 🔌 **Audio output** — a selector with **REFRESH** (re-enumerate the devices), **CHOOSE…** (browser output picker) and **System default** is part of the same dialog.

| Control | Action |
| :--- | :--- |
| ▶️ PLAY / ⏸ PAUSE | Play / pause |
| 🔴 CUE | Set (paused) or jump to the cue point; **SHIFT + CUE** clears it |
| ⚡ BEAT SYNC | Sync the deck to the other one |
| 🎡 Jog | Outer wheel = pitch bend, platter = scratch when touched / bend otherwise, **SHIFT + jog** = fast seek |
| 🎚️ TEMPO | Pitch fader and on-screen readout; the on-screen RANGE switch (±8% default / ±16%) also sets how far the hardware fader travels |
| 🔁 IN / OUT / 4 BEAT / ◁ ▷ | Loop in, loop out; **4 BEAT** exits an active loop (or sets a 4-beat one); **◁ ▷** halve / double the current loop |
| 🔢 Pads (HOT CUE) | Set or jump to hot cue 1-8; **SHIFT** clears it |
| 🎛️ Pads (PAD FX1 / PAD FX2) | Toggle delay, echo, flanger, reverb, phaser, bitcrush |
| ⏭️ Pads (BEAT JUMP) | Jump -16 / -8 / -4 / -1 / +1 / +4 / +8 / +16 beats |
| 🎤 Pads (SAMPLER) | Pads 1-4 mute / unmute vocal, instrumental, bass, drums in the same left-to-right order as the on-screen STEMS row; pads 5-8 toggle effects |
| 🎯 Pads (BEAT LOOP) | Set a 1/4 - 32 beat loop |
| 🎚️ TRIM / EQ / CFX | Trim, 3-band EQ and LP/HP filter (CFX) |
| 🔊 Channel fader / CH CUE | Volume and exclusive PFL |
| ↔️ CROSSFADER / MASTER | Crossfader and master level |
| 🎧 MASTER CUE | Exclusive PFL, mirrored on the master cue LED |
| 🎧 HEADPHONE MIX / LEVEL | Blend and level of the PFL bus |
| 🎛️ FX CH / SELECT / ON / LEVEL | CH1 / CH2 picks the deck targeted by FX SELECT, ON toggles its effect, LEVEL sets the shared depth |
| ◁ ▷ BEAT (FX section) | Beat jump both decks by one beat |
| 🧠 SMART CFX / SMART FADER | Toggle quantize / unmute all stems |
| 📂 BROWSE rotary | Scroll the selection through the Library track list (highlighted only while the controller is connected) |
| 📂 LOAD ◁ / ▷ | Load the selected Library track onto deck A / B (when the Library is open) |
| 📂 BROWSE press | Open or close the Library |
| 💡 LEDs | Play, cue, sync, loops, PFL, pad modes, pads, effects and master cue follow the app |

**Audio routing.** Every audio output of the system is listed in the dialog (the controller's USB interface is detected automatically and selected when found, **System default** is always available): VibeDJ sends the **master + PFL mix** there with `setSinkId`. A browser can only feed **one stereo stream to one output**, so both the controller's master outputs and its headphone jack carry that single mix, with **HEADPHONE MIX / LEVEL** blending PFL in; there is no separate cue channel. **REFRESH** re-reads the devices, **CHOOSE…** opens the browser's output picker, and the choice is remembered.

**Mapping.** The full MIDI map is a JSON object in the dialog: channels are 0-based (0 = MIDI channel 1), numbers are decimal MIDI notes / CC values, `0x` hex strings are accepted too, and every section can be overridden — `device` (name fragments), `channels`, `deck` (plus an optional `deckB` override), `fx`, `mixer`, `jogScale` and `leds` (`on` / `off` / `dim`). Edit it, press **APPLY** (saved in this browser) and **RESET** to restore the built-in map; invalid JSON is rejected with a toast.

---

## ⌨️ Keyboard shortcuts

VibeDJ is fully playable from the keyboard. ⌨️🎉

- 🪞 **Mirrored layout**: deck **A** uses the **left** half of the keyboard, deck **B** mirrors it on the **right**.
- 💬 Every control shows its key in its **tooltip** — just hover it. 🖱️
- 🎚️ **Analog controls**: press the control's key to **select** it, then use **↑ / ↓** to adjust.
- 🔠 Shortcuts are **case-sensitive** (e.g. `z` vs `Shift+Z` are different cues).
- 🎤 The **stems** use the **Alt** modifier (`Alt+1..4` on A, `Alt+7..0` on B), mirroring the effects layout.
- ⌨️ Keys are ignored while you are typing in a text field (Library search, key-map and MIDI editors).
- 🧭 `Esc` closes the open dialog or deselects the analog control; `Tab` stays inside an open dialog.

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
| ↘️↗️ Bend − / + (hold) | `-` / `+` | `r` / `è` |
| 🔊 Effects: delay / echo / flanger / reverb / phaser / bitcrush | `Shift+1..4` · `Shift+B` · `Backtick` | `Shift+7..0` · `Shift+N` · `=` |
| 🎤 Stems: vocal / instrumental / bass / drums | `Alt+1..4` | `Alt+7..0` |
| ⏭️ Beat jump −16 · −8 · −4 · +4 · +8 · +16 | `Shift+Q W E R T Y` | `Shift+U I O P { }` |
| 🎚️ Grid ÷2 · ×2 · nudge ◀ · ▶ · SET · TAP | `Shift+A S D F G H` | `Shift+J K L ; : "` |
| 🔇 Kill highs / mids / lows | `T G B` | `Y U N` |
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

> 🛠️ The whole keymap lives in a single **`SHORTCUT_CONFIG`** object in `index.html` — swap any key to build your own layout. ✏️ You can also remap everything **in-app**: open **How to use** (F2) and edit the **Custom key map** JSON (same shape: `deckA`, `deckB`, `mixer`, `global`), then press **APPLY**. The editor always opens filled with the map currently in use; unknown groups or fields and non-string values are rejected, and **APPLY** is blocked if a key is assigned to two actions (case matters), so you always get a conflict-free layout. The map is saved in `localStorage` and reloaded on every start (a stored map with conflicts is ignored at start-up). **RESET** restores and applies the built-in map, while **LOAD DEFAULT** only drops the built-in map into the editor so you can tweak it before pressing **APPLY**.
> ℹ️ Some slots (like **PFL** and **Trim**) are unassigned and shown as **`???`**; multiple `???` are allowed. In the deck-B layout **Kill mids** is `u` and **Bend −** is `r`.
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
| 🎨 | **HTML5 + CSS** (dark neon UI, Canvas rendering, CSS `zoom` for the UI scaling) |
| 🟨 | **Vanilla JavaScript** — zero dependencies, no build step |
| 🔊 | **Web Audio API** (graph of gains, biquads, delays, convolver, analysers) |
| 🎚️ | **AudioWorklet** — real-time `stem-dsp` processor for the stem split, with a biquad chain as fallback |
| 🧵 | **Web Workers** for BPM/beat analysis off the main thread (with a main-thread fallback) |
| 🎛️ | **Web MIDI API** + `setSinkId` for the controller and its audio output |
| 📂 | **File System Access API** (+ folder-input fallback) for the Library |
| 🎙️ | **MediaRecorder** for capturing the mix |
| 💾 | **localStorage** for the UI zoom, key map, MIDI map and audio output |
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

- ✅ Best in **Chrome / Edge** (File System Access API, MediaRecorder codecs, Web MIDI, audio-output routing).
- 🎛️ The **MIDI** section (DDJ-FLX4) needs **Chrome / Edge** for Web MIDI and `setSinkId`; other browsers keep mouse and keyboard control.
- 🎚️ The **stems** run in an **AudioWorklet**; where it is unavailable VibeDJ falls back to a biquad chain (lower separation quality).
- ✅ Works in **Firefox / Safari** with the Library's static-list fallback; the UI zoom relies on CSS `zoom`, implemented by current Chromium, Firefox and Safari.
- 🎧 A **headset** is recommended to use **PFL** headphone monitoring.

---

## 📜 License

Distributed under the **MIT License**. Feel free to use, modify, and share.

---

> 🌱 *Made with ❤️ and 🧠. If you find this tool helpful, please leave a ⭐ on GitHub!*
