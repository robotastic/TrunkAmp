# Trunkamp

A Winamp-style player interface for **Trunk Recorder Pro**, delivered as a single-file HTML application.

## Overview

Trunkamp provides a retro audio player interface for browsing, filtering, and playing live radio streams and recorded calls from Trunk Recorder Pro. The interface mimics the classic Winamp media player aesthetic while offering modern features tailored for radio monitoring and recording management.

## Features

### Core Playback Controls

- **Live Audio Stream**: Monitor live talkgroup audio at the top of the playlist
- **Recorded Calls**: Browse and play back previously recorded calls, oldest first
- **Playback Controls**:
  - **Play (X)** - Start playback from the current position or resume a paused call
  - **Pause (C)** - Pause live audio or recorded playback
  - **Stop (V)** - Stop playback entirely
  - **Previous (Z)** - Go to the previous call in playlist; from live, replay the last call heard
  - **Next (B)** - Go to the next call in playlist; from live, skip to the next available call

### Live Audio Management

- **HOLD Mode (S)** - Lock live audio to a specific talkgroup instead of scanning all channels
- **AUTO Mode (R)** - Automatically play new recordings as they arrive once the playlist finishes
- **Call Skipping** - Skip unwanted live calls and continue to the next transmission
- **Emergency Priority** - Prioritize emergency transmissions in live audio (configurable)

### Playlist Management

- **Dynamic Playlist**: Automatically populated with recorded calls from the recorder
- **Search & Filter (J)** - Filter calls by:
  - Talkgroup name or number
  - System name
  - Talkgroup description or group
- **Selection & Bulk Operations**:
  - **Click** - Select individual calls
  - **Ctrl/Cmd+Click** - Toggle selection
  - **Shift+Click** - Range selection
  - **SEL** - Toggle select all
  - **REM** - Remove selected calls from playlist view
  - **ADD (L)** - Open talkgroup picker to add calls to monitor
- **Sorting**: Calls are ordered chronologically (oldest first), with live audio pinned at top
- **Total Duration Display**: Shows selected vs. total duration of visible calls

### Audio Controls

- **Volume (↑ ↓)** - Adjust playback volume from 0-100%
- **Balance** - Stereo balance adjustment; double-click to center
- **Equalizer (Alt+G)** - 10-band parametric EQ optimized for voice clarity:
  - **Preamp** - Master gain control
  - **Frequency Bands**: 70 Hz, 150 Hz, 300 Hz, 500 Hz, 800 Hz, 1.2K, 1.6K, 2.2K, 3K, 3.6K
  - **Presets**:
    - Flat
    - Voice clarity
    - Cut hum and rumble
    - Tame harsh digital
    - Loud and clear
    - Telephone
  - **ON/OFF Toggle** - Enable/disable EQ processing

### Visualization & Display

- **LCD Display** - Shows elapsed/remaining time with 7-segment digit rendering
- **Time Modes** - Toggle between elapsed time and remaining time display
- **Visualizer** - Three modes:
  - **Spectrum** - Real-time frequency spectrum display
  - **Oscilloscope** - Waveform display
  - **Off** - Disable visualization
- **Marquee** - Scrolling text display of current call information

### Information & Details

- **Call Info (Alt+3)** - Detailed information about the currently selected call or live audio:
  - Talkgroup name and number
  - System name
  - Start time and duration
  - Frequency
  - Audio type and encoding
  - Emergency status
  - Encrypted/decrypted status
  - Signal and noise levels
  - Participating radio units/sources
- **About Window (O > About)** - Player information and quick reference

### Talkgroup Management

- **Open Talkgroup (L)** - Search and select specific talkgroups to monitor
- **Searchable Picker** - Find talkgroups by name, number, or system
- **Live Monitoring** - Switch to listening on selected talkgroup directly

### Context Menus

- **Right-click Calls** - Quick actions:
  - Play selected call
  - View call information
  - Download audio file
  - Listen to that talkgroup live
  - Filter to show only that talkgroup
  - Remove from playlist
- **Right-click Live** - Live audio options:
  - Play live stream
  - Open talkgroup picker
  - Release hold (return to scanning all)
  - View live call information

### Window Management

- **Draggable Windows** - Move any window around the interface
- **Window Docking** - Windows snap to each other's edges for organized layout
- **Shading** - Double-click title bar or click shade button to minimize windows
- **Toggle Visibility** - Show/hide equalizer and playlist windows
- **Layout Control**:
  - **Ctrl+D** - Double size (scales entire interface 2x)
  - Drag **GRIP** handle to resize playlist height
  - Automatic mobile layout for small screens
  - Reset window layout to defaults (Options menu)

### Seeking

- **Seek Bar (← →)** - Scrub through recorded calls
- **Seek Shortcuts** - Arrow keys for quick navigation

### Recording Control

- Start/stop recording directly from the Options menu (when connected to recorder)
- Connection status display

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| **Z** | Previous |
| **X** | Play |
| **C** | Pause |
| **V** | Stop |
| **B** | Next |
| **← →** | Seek |
| **↑ ↓** | Volume |
| **L** | Open talkgroup |
| **S** | Hold (lock to talkgroup) |
| **R** | Auto (auto-play new recordings) |
| **J** | Filter |
| **Alt+3** | Call info |
| **Alt+G** | Equalizer |
| **Alt+E** | Playlist |
| **Ctrl+D** | Double size |
| **Delete** | Remove selected calls |
| **Ctrl+A** | Select all |

## Configuration & Persistence

- **Settings** - All settings are saved to browser localStorage:
  - Volume and balance
  - Equalizer settings and presets
  - Window positions and sizes
  - Time display mode
  - Visualizer mode
  - Hold and Auto mode states
- **History** - Stores up to 1,000 recent calls for quick access

## Deployment

### Serve from Trunk Recorder Pro

```bash
trunk-pro --ui ./Interface → http://localhost:8080/
```

### Connect to Remote Recorder

Use the `?server=host:port` query parameter:

```
http://your-domain.com/trunkamp.html?server=recorder:8080
```

The page's origin must be added to the recorder's `allowedOrigins` configuration.

## Technical Details

### Audio Architecture

- **Web Audio API** - Modern audio processing and analysis
- **Live Streaming** - Real-time audio chunks from active calls
- **Recording Support** - Seamless playback of stored call audio
- **EQ Processing** - 10-band parametric filters optimized for voice frequencies (8 kHz sample rate)
- **Live Scheduler** - Intelligent scheduling of live audio chunks with gap detection
- **Analyzer** - Real-time spectrum and waveform analysis for visualization

### Supported Audio Formats

- **Live**: Real-time PCM audio streams from recorder
- **Recorded**: MP3, Opus, Codec2, and other formats supported by the recorder

### Encryption Support

- **Encrypted Calls** - Displays encrypted status; plays decrypted audio when available
- **Visual Indicators** - Encrypted calls shown with different styling in playlist

## Tips & Tricks

1. **Create Favorites** - Use the filter to search for frequently-monitored talkgroups, then monitor them via HOLD mode
2. **Bulk Cleanup** - Select multiple calls with Shift+Click, then REM to clean up the playlist
3. **Emergency Alerts** - Enable "Emergencies first (live)" in Options for priority alert handling
4. **Voice Quality** - Use the "Voice clarity" EQ preset for clearer intelligibility on noisy channels
5. **Mobile Use** - Interface automatically adapts to mobile screens; all controls remain accessible

## Troubleshooting

- **"AUDIO NOT AVAILABLE"** - The call's audio file was not kept by the recorder or failed to download
- **"CONNECTION FAILED"** - Verify the recorder URL and that your origin is in `allowedOrigins`
- **Live stream won't play** - Ensure HOLD is not locked to an inactive talkgroup
- **EQ not audible** - Toggle the EQ ON/OFF button to enable processing

## About

**Trunkamp** is a single-file interface designed for Trunk Recorder Pro. It combines the nostalgia of classic Winamp with modern web technologies to provide an intuitive, feature-rich monitoring and playback experience.

Recorder: Connect to **Trunk Recorder Pro** via the built-in web server
