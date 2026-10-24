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
- [📁 Loading tracks](#-loading-tracks)
- [📚 Library & 🧠 track analysis](#-library--track-analysis)
- [🎛️ The decks](#️-the-decks)
- [🌊 Overlaid waveform & beatgrid](#-overlaid-waveform--beatgrid)
- [🔊 Effects](#-effects)
- [🎤 Stems](#-stems)
- [🎯 Loops & hot cues](#-loops--hot-cues)
- [🎚️ The mixer](#️-the-mixer)
- [🎙️ Recording](#️-recording)
- [🎛️ DDJ-FLX4 controller](#️-ddj-flx4-controller)
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
| 🎛️ | **Pioneer DDJ-FLX4** controller support: full bidirectional MIDI mapping, LEDs and master audio routing |
| ⌨️ | Full **keyboard** control with on-screen tooltips |
| 🔍 | **UI zoom** — `−` / `+` buttons in the top bar resize the whole interface (30% → 120%): every element scales uniformly, waveform strip included, so nothing is cut off; when zoomed out the decks and mixer shrink while the waveform strip stretches vertically to fill all the remaining page space, leaving no empty gap at the bottom (modals, toasts and tooltips zoom too) |
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

- 📂 **SELECT FOLDER** — uses the modern **File System Access API** to browse a real folder and **REFRESH** it. 🔄 The list shows **only the playable audio files that sit directly in the selected folder**: subfolders are never listed and their content is not scanned.
- 🗃️ In browsers without that API, it falls back to a **static list** from a folder input (works in Chrome/Edge). 🧩 Same rule: only the files directly inside the picked folder are listed.

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
- 🅰️🅱️ **A / B** buttons → send the track to a chosen deck. The button stays lit in that deck's colour while the track is loaded there (and blinks while it is playing), so you always see where each track currently sits.
- 🪂 **Drag a row** → drop it onto a deck.
- ⏳ Analysis (BPM/key/energy) runs **in the background** in a **Web Worker**, so the UI never freezes. 🧵
- 🔃 **Sort** by clicking a column header (name / size / time / BPM / key / energy) — click again to flip the order.
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
- 💡 Shows the deck letter, a **beat-flash ring** and a scratch ring while scratching.

### 🚦 Transport
| 🎛️ Control | 🎬 Action |
| :--- | :--- |
| ⏮️ **START** | Jump back to the beginning |
| ▶️ **PLAY / ⏸️ PAUSE** | Start / stop playback |
| 🔴 **CUE** | Set the cue point; **hold** to preview from cue; press to snap back; **right-click** to clear the stored cue point — the button shows its amber colour only while a cue is stored, standard grey otherwise; the CUE text blinks while paused away from the cue point, like a real console |
| ⚡ **SYNC** | Match the other deck's tempo **and** beat phase |
| 🎚️ **TEMPO** fader | Change the tempo ±16% (also changes pitch — **no key lock**); oriented like the hardware, so sliding up slows down and sliding down speeds up |

### ⏭️ Beat jump & 🎚️ BPM/grid tools
- ⏭️ **Beat jump** — buttons `−16 · −8 · −4 · +4 · +8 · +16` jump whole beats (uses the detected BPM, defaults to 120 if none); with **QUANTIZE** on, the landing position snaps to the beatgrid.
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
- 🎨 Each half renders a **3-band colored waveform** (low / mid / high). The **hue follows the real band balance** — red for bass-driven passages, amber when bass and mids share the energy, green through the mids, cyan for mids + highs, blue for treble, violet when bass and highs dominate together — and every hue is lifted to the same **perceived brightness**, so low-frequency red sections are as readable as the mids and highs.
- 🪶 The strip is one **continuous filled contour**: the top and bottom edges are joined into a single path and the per-column colours are stretched underneath it as a 1-pixel colour row, instead of a row of separate bars. There are no flat-topped steps, the outline keeps its transients, and the per-column colours stay exact.
- 🎤 The strip follows the **stem mutes** (see [Stems](#-stems)): muting a stem attenuates the bands it belongs to, so the contour shows what you actually hear. The per-deck overview above the jog wheel always keeps the full mix.
- 💫 **No shimmer while playing**: the envelope is built from the peaks once and then **sampled with linear interpolation** at every column centre, so heights and hues are continuous functions of the playhead rather than being re-quantised for each frame. The whole contour simply slides with the track — frame-to-frame colour difference is ≈0.2 RGB units, against ≈9–16 when the columns were resampled every frame.
- 📊 **Track progress**: a thin strip along the top of each half shows the elapsed time over the whole track in the deck colour, with a bright cursor on the leading edge; it follows the real playback position (so it rewinds with a loop) and is display-only — seeking stays on the waveform below.
- 🥁 **Beatgrid**: the grid of the deck you're listening to is **solid**, the other deck's is **dashed**; the marked bar is the **downbeat** (every 4 bars).
- 📏 Each half displays the **phase offset in ms** against the beat — nudge the **TEMPO** fader until both grids stay locked. 🔒
- 🧭 A small **graphical phase meter** compares both decks' phase (it turns the deck color when the beats are aligned). 🎯

Each deck additionally has its own **overview waveform** canvas you can click to seek. 📊 On long tracks the colors come from the **average** band balance of each column (not the per-column peak): the hue is the **weighted mean of the three band colours** (red low, green mid, blue high), so warm amber marks bass-driven passages, green the mids, azure the hi-hat/sibilance sections and violet the parts where bass and treble carry the energy together without mids — a bass + treble column is never misread as green. Brightness is equalised per hue, so the low-frequency reds stay visible instead of sinking into a dark brown, and the height follows the **average energy** of the column, smoothed across neighbouring columns and drawn with generous headroom: the overview keeps a coherent palette and a readable envelope even when the whole track is squeezed into a few hundred pixels, and never clips to white.

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
| **VOCAL** | …the **centre** of the mix (mid = (L+R)/2) inside the **180 Hz – 4 kHz** band is removed from both channels through a dynamic **centre-dominance** mask: it only engages where the mid energy clearly exceeds the side energy and excludes drum transients, so centred vocals (fundamental → formants) drop while side-panned instruments, sibilants and air survive 🎙️ |
| **INST** | …the rest is removed: side content, non-centred mid and the band above 4 kHz, minus drum transients 🎹 |
| **BASS** | …the band below **180 Hz** is removed, except for drum attacks (the kick transient belongs to DRUMS) 🔉 |
| **DRUMS** | …drum transients are removed: the kick attack from the low band plus snare / hats / cymbals from the mid-high bands, leaving the kick body and sustain in BASS 🥁 |

The stems are applied **after** the effects chain (`… → phaser → bitcrush → stems → channel`). 🔗 Buttons are **colour-coded** — 🟣 vocal, 🟢 instrumental, 🔵 bass, 🟠 drums — and their background fills **only while the part is muted** (the mute is engaged); an audible part keeps the neutral button background. 🎛️

**🔁 Waveform feedback.** The shared **`syncWave`** strip redraws from what is still audible: each muted stem attenuates the bands it owns, so cutting the bass removes the low-frequency body of the contour while the kick transients survive in DRUMS, and cutting the drums flattens the transients and the air. The weights are a **frequency approximation** of the stem split, not the DSP gains:

| 🎚️ Stem muted (others on) | 🔉 Lows | 🎼 Mids | 🎼 Highs |
| :--- | :---: | :---: | :---: |
| **VOCAL** | 1.00 | 0.50 | 1.00 |
| **INST** | 1.00 | 0.68 | 0.55 |
| **BASS** | 0.12 | 1.00 | 1.00 |
| **DRUMS** | 0.88 | 0.82 | 0.45 |

With all four stems on, the strip shows the full mix exactly as before. The per-deck overview above the jog wheel stays on the full mix, so the two views answer different questions: "what does the track look like" and "what am I hearing right now". 👀

> ⚠️ These stems are a **frequency + transient approximation**, not machine-learning source separation. The signal is split into three bands with **4th-order Linkwitz-Riley** crossovers at **180 Hz** and **4 kHz**; the four stems are then derived with time-varying gains (centre-dominance for VOCAL, fast/slow envelope transient masks for DRUMS, kick attack vs bass sustain) and **sum back to the dry signal** — no inverted-cancellation comb filtering. The gains run at audio rate in an **AudioWorklet** (zero added latency, no model downloads), with the old biquad chain kept only as a fallback. With all stems on the deck is transparent (±0.1 dB). Measured with test tones: **BASS off** −21 dB at 100 Hz while 1 / 6 / 8 kHz stay at 0 dB; **VOCAL off** −34 dB at 1 kHz (centred) while air at 8 kHz moves −0.4 dB; **INST off** removes a side-panned 6 kHz tone entirely and −28 dB of centred air; **DRUMS off** on a kick removes the attack (1–16 ms) by −11.5 dB while the sustain (60–100 ms) stays within 0.7 dB and a steady bassline within 0.2 dB. On a **mono** track there is no centre to extract, so VOCAL mute is a no-op (INST/BASS/DRUMS still work); sibilance above 4 kHz is never assigned to VOCAL, which is why muting vocals leaves the "sss" in INST.

---

## 🎯 Loops & hot cues

### 🔁 Beat loops
- 🎚️ Quick presets: **1/4 · 1/2 · 1 · 2 · 4 · 8** beats (auto-sized from the detected BPM).
- ✂️ Manual **IN / OUT / EXIT** for free loop points.
- 🟢 The active loop highlights and playback wraps seamlessly. 🔄
- 📌 Changing the loop length of an **existing** loop (preset buttons, FLX4 pads or knob) keeps the original **IN** point and only moves the **OUT** — the loop grows or shrinks around its own start instead of jumping to the current position.

> 🎯 Turn on **QUANTIZE** (switch next to the PHONES knob in the mixer) to snap cue points, loops, hot cues and beat jumps to the nearest beat. ✨

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
| **FILTER** 🌊 | Bipolar **LP / HP** filter (low-pass down to ~200 Hz, high-pass up to ~2 kHz); LP values of 1 kHz or more are shown compactly, e.g. `18.2k` |
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

## 🎛️ DDJ-FLX4 controller

Press **FLX4** in the top bar to connect a **Pioneer DDJ-FLX4** over USB (Web MIDI, Chrome / Edge). The full surface is mapped and **bidirectional**: moving a control updates the interface, and the interface (including keyboard shortcuts) lights up the controller LEDs. Press the button again to disconnect.

| Control | Action |
| :--- | :--- |
| ▶️ PLAY / ⏸ PAUSE | Play / pause |
| 🔴 CUE | Set (paused) or jump to the cue point; **SHIFT + CUE** clears it |
| ⚡ BEAT SYNC | Sync the deck to the other one |
| 🎡 Jog | Outer wheel = pitch bend, platter = scratch when touched / bend otherwise, **SHIFT + jog** = fast seek |
| 🎚️ TEMPO | Pitch fader (±16%) and on-screen readout |
| 🔁 IN / OUT / 4 BEAT / ◁ ▷ | Loop in, loop out, 4-beat loop or exit, halve / double the loop |
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

**Audio routing.** The FLX4's built-in USB audio interface shows up as an extra output: VibeDJ can send the **master + PFL mix** to it with `setSinkId`. A browser can only feed **one stereo stream to one output**, so both the controller's master outputs and its headphone jack carry that single mix, with **HEADPHONE MIX / LEVEL** blending PFL in; there is no separate cue channel. Choose the output in the FLX4 dialog (the controller is detected automatically) or with **CHOOSE…**; the choice is remembered.

**Mapping.** The full MIDI map is a JSON object in the FLX4 dialog: channels are 0-based, values are decimal MIDI notes / CC numbers, and `0x` hex strings are accepted too. Edit it, press **APPLY** (saved in this browser) and **RESET** to restore the built-in map. Close rekordbox and any other app holding the controller's MIDI port before connecting.

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

> 🛠️ The whole keymap lives in a single **`SHORTCUT_CONFIG`** object in `index.html` — swap any key to build your own layout. ✏️ You can also remap everything **in-app**: open **How to use** (F2) and edit the **Custom key map** JSON (same shape: `deckA`, `deckB`, `mixer`, `global`), then press **APPLY**. The map is saved in `localStorage` and reloaded on every start; **APPLY** is blocked if a key is assigned to two actions (case matters), so you always get a conflict-free layout. **RESET** restores the built-in map.
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
- 🎛️ The **DDJ-FLX4** needs **Chrome / Edge** (Web MIDI and audio-output routing); other browsers keep mouse and keyboard control.
- ✅ Works in **Firefox / Safari** with the Library's static-list fallback.
- 🎧 A **headset** is recommended to use **PFL** headphone monitoring.

---

## 📜 License

Distributed under the **MIT License**. Feel free to use, modify, and share.

---

> 🌱 *Made with ❤️ and 🧠. If you find this tool helpful, please leave a ⭐ on GitHub!*
