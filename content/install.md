+++
date = '2025-10-15T13:10:14+09:00'
draft = false
title = 'Installation Guide'
+++

# NicolNavi Installation Guide

This guide walks you through getting NicolNavi up and running in a Python environment. Review the checklist below before you start.

## Before You Begin

- Supported systems: Windows 10 (64-bit) or later, macOS Monterey (12) or later, and popular Linux distributions
- Permissions: Administrator rights may be required during the initial setup
- Browser: Latest Google Chrome (recommended)
- Memory: 16 GB RAM or more is strongly recommended; lower-spec systems may not run reliably

{{< notice info >}}Other browsers might work, but only Google Chrome is officially verified.{{< /notice >}}

---

## Installing with a Python Environment

### Step 1. Confirm Prerequisites

1. **Google Chrome**  
   Install it from the link above if you have not already.
2. **Python and pipenv**  
   Ensure Python 3.10 or newer is installed and that the `pip` command works. Update pip with `pip install --upgrade pip`, then install pipenv using `pip install pipenv`.

### Step 2. Download NicolNavi

1. Grab the ZIP archive from https://github.com/Tan-Furukawa/nicolnavi and extract it.
2. Open a terminal and move into the project directory.

```bash
cd /path/to/nicolnavi
```

### Step 3. Set Up the Virtual Environment

1. Run the following commands to create and populate a pipenv environment:

```bash
pipenv shell
pipenv install
```

2. Wait for `Pipfile.lock` to be generated and dependency installation to finish.

{{< notice info >}}The prompt should show the virtual environment name—typically something like `(nicolnavi)`. Type `exit` to leave the environment when you are done.{{< /notice >}}

### Step 4. Launch the Application

1. With the pipenv shell still active, start the UI:

```bash
python gui/src/main.py
```

2. Open Google Chrome and go to `http://localhost:8551/` to confirm that NicolNavi loads.

---

## Troubleshooting

- **Nothing loads in the browser**: Make sure `python gui/src/main.py` is still running. Restart it if necessary.
- **Port 8551 already in use**: Another application is occupying the port. Stop that application or adjust NicolNavi’s port setting.
- **`pipenv install` fails**: Run `pipenv --rm` to remove the environment and repeat Step 3.

If you encounter issues you cannot resolve, note any error messages and contact the development team for assistance.
