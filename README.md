# OCA GEM Tool

**SECS/GEM Communication Simulator & Testing Tool**

A browser-based interactive tool for simulating, testing, and visualizing SEMI SECS/GEM semiconductor equipment communication protocols. Runs as a single standalone executable — no Python, Node.js, or other runtime required.

![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11%20(x64)-blue)
![Standards](https://img.shields.io/badge/SEMI-E30%20%7C%20E37-green)
![License](https://img.shields.io/badge/license-proprietary-lightgrey)

---

## 🎯 Motivation & Background

At its core, SECS/GEM communication is simply a matter of managing state transitions and string-based data exchanges. However, due to varying interpretations of the SEMI standards and their inherent vastness, engineers are often forced into overly complex implementations.

Spending excessive time and implementation costs just to build these fundamentally simple structures is a root cause of stagnation in the manufacturing automation industry. 

The primary goal of this project is the **democratization of SECS/GEM**. By opening up this traditionally closed and complicated domain, we aim to free engineers from endless communication debugging, allowing them to focus on what truly matters: the core machine control logic.

---

## ✨ Features

### 🔌 HSMS/SECS-II Protocol (SEMI E37)
- **Active (Equipment) + Passive (Host)** HSMS TCP connections
- Select / Deselect / Linktest / Separate control messages
- SECS-II message encoding/decoding with real-time hex & structured view
- Auto-respond for common messages (S1F1, S1F13, S6F11, Select.req)

### 📊 GEM State Machine Visualization (SEMI E30)
- **5-layer state machine** with interactive SVG diagrams:
  - **HSMS** — TCP connection & session management
  - **Communication** — Establish Communication (S1F13/S1F14)
  - **Control** — Equipment Online/Offline/Local/Remote
  - **Process** — Processing state lifecycle (INIT → SETUP → READY → EXECUTING → ...)
  - **Spooling** — Message spooling management
- Layer dependency bar showing the HSMS → Communication → Control → Process → Spooling cascade
- **State Sync Matrix** — real-time Equipment vs Host state comparison per layer

### 🖥️ Dual-Panel Architecture
| Equipment (Left) | Host / Server (Right) |
|---|---|
| State Machine owner (Active HSMS) | Observer / Request side (Passive HSMS) |
| GEM Equipment simulation | GEM Host simulation |
| Event triggering, Alarm reports | S2F33/S2F35/S2F37/S2F41 commands |
| Manual state transitions | Manual state transitions |

### 🧪 Scenario Runner
- Load and execute JSON-based test scenarios
- Automated state machine verification per step
- Phase-based execution with PASS/FAIL per step
- Built-in scenarios:
  - **GEM-NORMAL-001** — Normal communication establishment & processing flow
  - **GEM-HSMS-ERROR-001** — Error handling (connection loss, timeout, reject)
- Supports both English and Japanese scenario files
- Custom scenario upload via UI

### ⚙️ GEM Configurator
- Define **Variables** (VID) with SECS-II data types (U1–U4, I1–I4, ASCII, Boolean, etc.)
- Define **Reports** (RPTID) — group variables into report structures
- Define **Events** (CEID) — link events to reports
- JSON Import / Export
- Push configuration to running engine in real-time

### 🌐 Internationalization (i18n)
- English / Japanese UI switching
- All labels, messages, and tooltips are translatable

### 📟 Terminal / Message Log
- Real-time SECS-II message log with timestamps
- Send/Receive direction indicators
- Raw hex display for protocol debugging

---

## 📋 System Requirements

| Item | Requirement |
|---|---|
| OS | Windows 10 / 11 (64-bit) |
| Browser | Chrome / Edge (recommended) |
| Runtime | None (self-contained C++ binary) |
| Ports | 8420 (HTTP) + 8421 (WebSocket), configurable |

---

## 🚀 Quick Start

### 1. Download

Download the latest release ZIP from the [Releases](../../releases) page.

### 2. Extract & Launch

```text
oca_gem_tool_vX.XXXX.XXXX/
├── launch.bat                  ← Double-click to start
├── oca_gem_tool_engine.exe     ← C++ standalone engine
├── index.html                  ← Web UI
├── css/
├── js/
├── scenarios/                  ← Built-in test scenarios
├── sample/                     ← Sample GEM configuration
└── version.txt
