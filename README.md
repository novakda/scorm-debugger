# SCORM Debugger — TASBot for eLearning

A Vue.js debugging harness for SCORM courses with emulator-style save state functionality. Test gated eLearning content in minutes instead of hours.

**Live case study:** [Exhibit M — pattern158.solutions](https://pattern158.solutions/exhibits/exhibit-m.html)

---

## The Problem

Testing gated eLearning courses — completion-gated or assessment-gated — requires manually clicking through every section to reach the part you actually need to test. Hours per QA cycle, repeated for every bug and every regression check.

This is the same problem speedrunners solved decades ago with **emulator save states**: instead of replaying from the beginning every time, save the state and restore it instantly.

## The Solution

A Vue.js wrapper that provides a fake SCORM runtime environment. Courses run inside it as if they were in a real LMS — but with full state control:

- **Save state** at any point in the course
- **Restore** any previous state instantly — no replay from the beginning
- **Edit SCORM values** directly: completion status, score, suspend data
- **Jump** to any section regardless of gating logic
- **Inspect** real-time SCORM API calls as they happen

Testing cycles drop from hours to minutes for gated content.

## Why This Exists

Commercial SCORM tools (SCORM Cloud, SCORM Engine) excel at runtime conformance testing. But **reproducible debug states** — the ability to save, restore, and edit course state for targeted testing — are not first-class features in any of them.

This tool fills that gap from the integrator's side.

## The TASBot Parallel

Tool-Assisted Speedrunning (TAS) uses emulator save states to achieve frame-perfect optimization — saving at any point, restoring instantly, testing every branch without replaying from the start. SCORM Debugger applies the same methodology to eLearning QA:

- Save state = serialize current SCORM session to JSON snapshot
- Restore state = deserialize snapshot, reinitialize course at exact point
- Frame-perfect testing = targeted scenario reproduction without full playthrough

## Architecture
```
src/
  api/              # SCORM API emulation layer (1.2 and 2004)
  components/       # Debugger UI — state inspector, editor, save/restore controls
  composables/      # State serialization, course communication hooks
  wrapper/          # Course iframe wrapper and message bridge
```

## Status

🚧 **Active rebuild** — Original tool built at GP Strategies (~2019-2020). This is a clean public reconstruction with improved architecture.

- [x] Repository scaffold and documentation
- [ ] SCORM 1.2 API stub
- [ ] SCORM 2004 API stub
- [ ] State serialization / deserialization
- [ ] Save / restore UI
- [ ] SCORM value editor
- [ ] Real-time API call inspector
- [ ] Course iframe wrapper

## Tech Stack

- **Vue 3** with Composition API
- **TypeScript**
- **Vite**
- SCORM 1.2 and SCORM 2004 API emulation

## Development
```bash
npm install
npm run dev
```

## Background

Built during internal tooling work at GP Strategies Corporation. The organizational context — a direct-labor billing model with no budget category for internal tooling — meant the tool was never fully polished or formally adopted despite clear ROI. The full story is documented in [Exhibit M](https://pattern158.solutions/exhibits/exhibit-m.html).

The tool functions as a **culture-fit diagnostic**: organizations that invest in developer productivity are the right environment for this kind of work.

---

*Part of the [Pattern 158 Solutions](https://pattern158.solutions) portfolio.*
