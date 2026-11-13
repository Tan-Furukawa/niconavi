+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'Installation Guide'
+++

# NicolNavi Installation Guide

Download the appropriate package for your system from [GitHub Releases](https://github.com/Tan-Furukawa/niconavi_app/releases).

## Windows

Download and run `NicoNavi-Setup.exe`, then follow the installer instructions.

## Linux (x86_64 AppImage)

Download `NicoNavi-<version>-x86_64.AppImage`, make it executable in Terminal, and run it.

```bash
chmod +x NicoNavi-*-x86_64.AppImage
./NicoNavi-*-x86_64.AppImage
```

## Python (macOS and other platforms)

Install [uv](https://docs.astral.sh/uv/) and Git, then run the following commands in Terminal or PowerShell. This method also works on Windows and Linux.

```bash
git clone https://github.com/Tan-Furukawa/niconavi_app.git
cd niconavi_app
uv sync --frozen
uv run python niconavi.py
```
