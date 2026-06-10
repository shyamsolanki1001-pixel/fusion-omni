# FUSION OMNI

> An ambient AI desktop assistant for Windows. Not a chatbot. An operating layer.

**[â†’ Live Showcase](https://shyamsolanki1001-pixel.github.io/fusion-omni)**

---

## What is Omni

Omni is a persistent background process that runs on your Windows machine and actually knows what's happening on your screen. It doesn't wait to be opened â€” it's already there. It reads your active UI tree, listens for your voice, tracks context across sessions, and responds through a transparent always-on-top HUD overlay styled after a Jarvis-grade system interface. Think less "AI chatbot in a tab" and more "AI that lives in your OS."

It's opinionated by design. Omni has a defined character â€” epistemically dry, precise, capable of genuine disagreement. It won't tell you what you want to hear.

---

## Architecture

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                   FUSION OMNI CORE                   â”‚
â”‚                                                      â”‚
â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”  â”‚
â”‚  â”‚  Audio   â”‚   â”‚   Screen     â”‚   â”‚   Webcam    â”‚  â”‚
â”‚  â”‚ Pipeline â”‚   â”‚ Intelligence â”‚   â”‚  Perception â”‚  â”‚
â”‚  â”‚ PyAudio  â”‚   â”‚  WinUIAuto   â”‚   â”‚   OpenCV    â”‚  â”‚
â”‚  â”‚ Whisper  â”‚   â”‚  + OpenCV    â”‚   â”‚             â”‚  â”‚
â”‚  â””â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”˜   â””â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”˜   â””â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”˜  â”‚
â”‚       â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜          â”‚
â”‚                        â–¼                             â”‚
â”‚              â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                    â”‚
â”‚              â”‚    LangGraph     â”‚                    â”‚
â”‚              â”‚   Agent Graph    â”‚                    â”‚
â”‚              â”‚ (multi-agent     â”‚                    â”‚
â”‚              â”‚  orchestration)  â”‚                    â”‚
â”‚              â””â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                    â”‚
â”‚                       â–¼                              â”‚
â”‚              â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”                    â”‚
â”‚              â”‚   Claude API     â”‚                    â”‚
â”‚              â”‚ (reasoning +     â”‚                    â”‚
â”‚              â”‚  character)      â”‚                    â”‚
â”‚              â””â”€â”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜                    â”‚
â”‚       â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”              â”‚
â”‚       â–¼               â–¼               â–¼              â”‚
â”‚  â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”   â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”      â”‚
â”‚  â”‚  PyQt6  â”‚   â”‚Persistentâ”‚   â”‚   Thermal    â”‚      â”‚
â”‚  â”‚   HUD   â”‚   â”‚  Memory  â”‚   â”‚   Safety     â”‚      â”‚
â”‚  â”‚ Overlay â”‚   â”‚  Layer   â”‚   â”‚Infrastructureâ”‚      â”‚
â”‚  â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜   â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜   â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜      â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

See [`docs/architecture.md`](docs/architecture.md) for the full technical breakdown.

---

## Tech Stack

| Subsystem | Technology | Purpose |
|---|---|---|
| HUD Overlay | PyQt6 | Frameless transparent always-on-top window. Click-through. Cyan/black aesthetic |
| Agent Orchestration | LangGraph | Multi-agent graph â€” intent parsing, tool routing, self-correction loops |
| Screen Intelligence | Windows UI Automation + OpenCV | Live UI tree parsing, active window context, visual awareness |
| Audio Pipeline | PyAudio + OpenAI Whisper | Continuous microphone monitoring, ambient voice detection, STT |
| Core Reasoning | Claude API (Anthropic) | Primary intelligence, character, nuanced multi-step reasoning |
| Webcam Perception | OpenCV | Ambient visual context pipeline |
| Persistent Memory | Custom layer | Cross-session context, user preferences, working memory |
| Thermal Safety | Custom monitoring | CPU temp tracking, throttle detection, load management |

---

## Build Status

| Subsystem | Progress |
|---|---|
| HUD Overlay | ![85%](https://progress-bar.dev/85?title=HUD+Overlay&color=00bcd4) |
| Agent Orchestration | ![72%](https://progress-bar.dev/72?title=Agent+Orchestration&color=00bcd4) |
| Screen Intelligence | ![60%](https://progress-bar.dev/60?title=Screen+Intelligence&color=00bcd4) |
| Audio Pipeline | ![55%](https://progress-bar.dev/55?title=Audio+Pipeline&color=00bcd4) |
| Persistent Memory | ![40%](https://progress-bar.dev/40?title=Persistent+Memory&color=00bcd4) |
| Thermal Safety | ![90%](https://progress-bar.dev/90?title=Thermal+Safety&color=00bcd4) |

---

## Why I built this

I wanted a Jarvis. An actual one â€” not a voice assistant that sets timers, not a chatbot that forgets you exist between sessions. Something that genuinely knows the context of what I'm doing and can operate at the OS level without me babysitting it constantly. I looked for something like that. It didn't exist. So I started building it instead, outside of coursework, on a laptop that has since been pushed to its thermal limits several times in service of this goal.

It's a first-year project. That's not a caveat â€” it's the point.

---

## Status

**Current version:** `v0.9 â€” Pre-release`

**What's working:**
- HUD overlay renders, floats, and animates correctly over arbitrary windows
- LangGraph agent graph executes multi-step reasoning chains
- Windows UI Automation successfully reads live UI tree from active applications
- Whisper pipeline loads and processes microphone input
- Thermal monitoring active with automatic warning system

**In progress:**
- Persistent memory cross-session retrieval
- Webcam context integration with reasoning pipeline
- Audio wake-word reliability improvements
- Full agent self-correction loops

---

## Project Structure

```
fusion-omni/
â”œâ”€â”€ docs/
â”‚   â”œâ”€â”€ architecture.md    â€” subsystem design and agent graph
â”‚   â”œâ”€â”€ build-log.md       â€” reverse-chronological dev journal
â”‚   â””â”€â”€ character.md       â€” Omni's personality specification
â”œâ”€â”€ index.html             â€” live showcase page
â”œâ”€â”€ .gitignore
â”œâ”€â”€ LICENSE
â””â”€â”€ README.md
```

---

<p align="center">
  <a href="https://github.com/shyamsolanki1001-pixel/fusion-omni/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License">
  </a>
  <img src="https://img.shields.io/badge/status-pre--release-orange.svg" alt="Pre-release">
  <img src="https://img.shields.io/badge/python-3.12-blue.svg" alt="Python 3.12">
  <img src="https://img.shields.io/badge/platform-Windows-lightgrey.svg" alt="Windows">
</p>

<p align="center">
  <sub>Â© 2025 Shyam Solanki â€” De Montfort University, Leicester</sub>
</p>
