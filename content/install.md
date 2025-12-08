+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'Installation Guide'
+++

# NicolNavi Installation Guide

## Requirements
- uv (Python package manager)
- Google Chrome (recommended)

## Install uv

### macOS / Linux
1. Open Terminal.
2. Run `curl -LsSf https://astral.sh/uv/install.sh | sh`.
3. Close Terminal.

### Windows (PowerShell)
1. Open PowerShell.
2. Run `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`.
3. Close PowerShell.

## Set up NicolNavi

1. Open https://github.com/Tan-Furukawa/niconavi_app.
2. Click `Code` → `Download ZIP`, then extract the ZIP to any location.

### macOS
1. Right-click the extracted `niconavi_app` folder → Service → New Terminal tab at Finder (or otherwise open Terminal in that folder).
2. In Terminal, run:

   ```
   chmod 777 ./run_niconavi_mac.sh
   ./run_niconavi_mac.sh
   ```

### Windows
Double-click `run_niconavi_Windows.bat`.

- The required Python environment installs automatically. When installation finishes, Google Chrome will launch and NicolNavi will start. **On the first install, startup can take up to about 5 minutes. Even if Chrome shows `This site can’t be reached`, please wait.**
- Use the same steps to start the app next time; subsequent launches are faster. The `chmod 777` command is only needed the first time.

## Manual workflow
- Install deps: `uv sync`
- Run app: `uv run python niconavi.py`
- App URL: `http://localhost:8551/app`
