# Omni â€” Build Log

> Reverse-chronological. Written as things happened, not as I wished they had.

---

## 2025 â€” November

### Nov 20 â€” Multi-agent graph stable. Finally.

Three weeks of LangGraph state management hell. The problem kept shifting: first it was state mutation across nodes (LangGraph's `TypedDict` model is opinionated about this in ways the docs don't fully surface), then it was the corrector node creating infinite retry loops on edge cases I hadn't anticipated, then it was message serialisation breaking when the context payload exceeded a certain size.

It clicked on a Thursday afternoon. The relief was physical â€” I actually sat back from the desk. The graph ran end-to-end, routed correctly, self-corrected on a deliberately bad input, and produced a coherent response. I ran it again six times to make sure it wasn't a fluke.

It wasn't a fluke.

**What I fixed:** State mutation model reworked to immutable updates. Corrector node now has a hard retry cap (2) with a fallback path. Context payload compression for large screen snapshots.

---

## 2025 â€” October

### Oct 8 â€” HUD overlay: first successful render

This one took longer than it should have. PyQt6 frameless transparent window is straightforward in isolation â€” the documentation covers it. The problem is making it *stay* transparent and click-through while overlaying real applications, including applications that use hardware-accelerated rendering.

The solution was setting `WS_EX_LAYERED | WS_EX_TRANSPARENT` via ctypes directly after the Qt window handle was created. Qt's own transparency flags don't fully cover the Windows-specific behaviour needed for click-through on DX12 surfaces.

When it first appeared floating over my desktop I didn't say anything for about thirty seconds. Just looked at it. That was a good thirty seconds.

**Stack at this point:** PyQt6 + ctypes for WinAPI flags + IPC socket to receive render commands from the main process.

---

## 2025 â€” September

### Sep 14 â€” Thermal crisis mitigated (KLIM Cyclone cooling pad, stage 1)

The laptop was hitting 95Â°C under sustained model inference. Not occasionally â€” consistently. CPU clock was collapsing from 2.4GHz to 400MHz under thermal throttle, which made inference latency wildly unpredictable and basically unusable for real-time response.

Ordered a KLIM Cyclone cooling pad at 2am. Arrived next day. Dropped the sustained temp by 22Â°C under the same load. Inference latency became predictable again.

This was a temporary fix. The proper solution is thermal repaste (still on the list) and working within BIOS power limits rather than against them. The Gigabyte OEM BIOS locks power limit configuration â€” I cannot modify this in software. The thermal watchdog infrastructure I built around this constraint is now the most reliable subsystem in the project.

Lesson: build thermal monitoring before building anything fun. I built it after. Don't do that.

**Permanent mitigations in place:**
- Thermal watchdog polling CPU package temp every 5s via `wmi`
- Hard inference suspension at 95Â°C with mandatory cooldown
- Cooling pad (hardware)
- Professional repaste scheduled

---

### Sep 3 â€” Windows UI Automation working on live applications

Getting the accessibility tree from arbitrary applications is inconsistent by design. Well-behaved apps (most Microsoft ones, most Electron apps) expose clean trees. Everything else is a gamble.

The approach that actually works: try the UIAutomation COM interface first with a 500ms timeout. If the tree comes back empty or with only root elements, fall back to an OpenCV screenshot + Tesseract OCR pass. The OCR is slower and less structured but it gets *something*.

The screen snapshot is now injected into every agent call. Omni seeing what I'm looking at makes a noticeable difference to response relevance.

---

## 2025 â€” August

### Aug 3 â€” Git workflow. Embarrassingly late.

Two months of single-file chaos before this. I was editing `omni_main.py` directly with no version control, saving "backups" with names like `omni_main_WORKING_DO_NOT_DELETE.py`. That file existed in four variants by this point, none of which were clearly the most recent.

Set up a proper repository, did an initial commit of whatever was actually running at the time, established branch discipline. It's remarkable how much faster development became when I wasn't afraid to change things.

At least the mistakes are versioned now. Future me will be grateful.

---

## 2025 â€” July

### Jul 19 â€” The thermal incident (original)

Pushed inference too hard, too long, with no monitoring in place. Fan ramped to maximum. CPU throttled to 400MHz. Laptop was effectively unusable for about 20 minutes while it cooled.

This was the event that triggered the thermal safety infrastructure. Everything above (the September entry) is the consequence of this moment. At the time I was annoyed. In retrospect: good. It happened early enough that I could architect around it.

**What I was running:** A Whisper inference loop + a LangGraph execution + a PyQt6 process + a background screen capture thread. All simultaneously, on a mid-range consumer laptop, with no load management. This was not a good idea.

---

## 2025 â€” June

### Jun 1 â€” The idea crystallises

I wanted a Jarvis. Not "Siri but better" â€” an actual ambient, persistent, OS-aware assistant that knew what I was doing and could operate at a level above individual applications. I looked for something like that for about two weeks. Nothing came close.

The closest things I found were demo projects â€” impressive for a YouTube video, useless as a daily driver. Either they required a bespoke hardware setup, or they were just a chat interface with a screenshot attached, or they were a voice assistant that could do exactly four things.

I thought: how hard can it be.

The answer, as it turns out, is: considerably. I started anyway.

**First working code:** A PyAudio loop that captured microphone input and wrote it to a file. Not impressive. It was a start.

---

*This log will keep going as long as the project does.*
