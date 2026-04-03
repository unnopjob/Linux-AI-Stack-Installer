# Ubuntu AI Stack Installer

`Ubuntu AI Stack Installer` is a Bash installer for Ubuntu that sets up:

- Ollama
- `gemma2:9b`
- Node.js
- Flowise
- PM2 startup for Flowise on boot/reboot
- Optional swap file
- Optional PM2 log rotation
- Desktop and app-menu launchers for Flowise and the installer

## Files

- `install.sh` is the canonical installer
- `install-ubuntu-ai-stack.sh` is a compatibility wrapper that points to `install.sh`

## Quick Start

### Option 1: run from a local copy

```bash
chmod +x install.sh
./install.sh
```

### Option 2: run directly from GitHub

```bash
curl -fsSL https://raw.githubusercontent.com/unnopjob/install-ubuntu-ai-stack/main/install.sh | bash -s --
```

When you run it in a terminal, long steps show a live spinner automatically and the installer tags phases as `[1/8]`, `[2/8]`, and so on.

## Extra Commands

```bash
./install.sh --status
./install.sh --open-flowise
```

If you run from GitHub and want to pass a command, use the same `bash -s --` form:

```bash
curl -fsSL https://raw.githubusercontent.com/unnopjob/install-ubuntu-ai-stack/main/install.sh | bash -s -- --status
```

## Optional Overrides

You can tweak the install with environment variables:

```bash
OLLAMA_MODEL=gemma2:9b FLOWISE_PORT=3000 NODE_MAJOR=24 ./install.sh
```

If you want to skip the short `gemma2:9b` smoke test after download:

```bash
RUN_MODEL_SMOKE_TEST=0 ./install.sh
```

To enable swap creation and PM2 log rotation:

```bash
ENABLE_SWAP=1 SWAP_SIZE_GB=8 ENABLE_PM2_LOGROTATE=1 ./install.sh
```

If you do not want the installer to create desktop and app-menu launchers:

```bash
CREATE_DESKTOP_LAUNCHER=0 ./install.sh
```

If you want to disable the live spinner output:

```bash
SPINNER_ENABLED=0 ./install.sh
```

If you mirror the script somewhere else, override the raw URL:

```bash
INSTALLER_URL=https://raw.githubusercontent.com/<user>/<repo>/main/install.sh ./install.sh
```

## After Install

- Flowise opens at `http://localhost:3000`
- Ollama API is at `http://localhost:11434`
- PM2 will restore Flowise automatically after reboot
- The installer creates `~/.local/bin/open-flowise`
- The installer creates `~/.local/bin/install-ai-stack`
- The installer adds `.desktop` files for both launchers when a desktop is available

## Notes

- The script is written for Ubuntu or other Debian-based Linux systems that use `systemd`
- `gemma2:9b` is a fairly large model, so make sure the machine has enough RAM and disk space
- If you want to expose Flowise beyond `localhost`, add a reverse proxy and authentication first
