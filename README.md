# NEXUS — System Intelligence Engine

A lightweight C++17 terminal system monitor that turns live machine stats into a readable developer dashboard. It displays CPU usage, RAM usage, a short CPU history, the top memory-consuming processes, and high-usage warnings.

> **Built with:** C++17, STL, OS-level system APIs, CMake  
> **Platforms:** Windows 10/11 and Linux  
> **Privacy:** all readings are collected locally; nothing is uploaded.

## Features

- Live CPU usage with a rolling text history
- RAM usage in percentage and GB
- Top 8 processes by resident/working-set memory
- High CPU/RAM warnings at 85%
- Configurable refresh interval
- One-shot mode for scripts and debugging
- No external dependencies

## Preview

```text
  NEXUS
  SYSTEM INTELLIGENCE ENGINE | Refresh: 2s

  CPU   [##########--------------]  42.7%
  RAM   [##############----------]  58.1%   9.3 / 16.0 GB

  CPU HISTORY (last 8 samples)
    .:-=+*#

  TOP PROCESSES BY MEMORY
  PID     PROCESS                     RAM (MB)
  -----------------------------------------------
  1840    browser.exe                  1240.2
  5012    Code.exe                      840.7
```

Numbers above are illustrative, not measured output.

## Build

### Windows (Visual Studio Build Tools + CMake)

Install a C++ compiler and CMake. From the project directory:

```powershell
cmake -S . -B build
cmake --build build --config Release
.\build\Release\nexus.exe
```

If using a single-configuration generator such as MinGW Makefiles:

```powershell
cmake -S . -B build -G "MinGW Makefiles"
cmake --build build
.\build\nexus.exe
```

### Linux

Install `g++` and CMake, then run:

```bash
cmake -S . -B build
cmake --build build -j
./build/nexus
```

## Usage

```bash
nexus
nexus --once
nexus --interval 5
nexus --help
```

- `--once`: print one snapshot and exit
- `--interval SECONDS`: refresh between 1 and 60 seconds (default: 2)
- `--help`: print usage

## How it works

- **Windows:** `GetSystemTimes`, `GlobalMemoryStatusEx`, Tool Help process snapshots, and process working-set counters.
- **Linux:** `/proc/stat`, `/proc/meminfo`, `/proc/<pid>/statm`, and `/proc/<pid>/comm`.
- **C++:** STL containers, sorting, formatting, command-line parsing, signal handling, and platform-specific compilation.

## Roadmap

Ideas for meaningful next releases:

- [ ] CSV logging and session reports
- [ ] Per-process CPU usage
- [ ] Config file and custom alert thresholds
- [ ] JSON output for scripts
- [ ] Terminal color themes and keyboard controls
- [ ] Unit tests for parsing and metric calculations
- [ ] macOS support

## Contributing

Issues and pull requests are welcome. Keep changes small, explain the reason for the change, and include build/test steps.

## License

MIT — see [LICENSE](LICENSE).
