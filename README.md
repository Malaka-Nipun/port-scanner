# PortScan

A fast TCP port scanner with two interfaces — a terminal-style **web UI** that runs in the browser, and a **Python CLI** tool for full TCP scanning.

![License](https://img.shields.io/badge/license-MIT-green) ![Python](https://img.shields.io/badge/python-3.8+-blue) ![No dependencies](https://img.shields.io/badge/dependencies-none-brightgreen)

---

## Live Demo

**[yourusername.github.io/port-scanner](https://yourusername.github.io/port-scanner)**

---

## Features

- Scan any host by IP or domain name
- Port presets — `web`, `db`, `common`, `ssh`, `http`
- Custom port ranges — `22`, `80,443`, `1-1024`
- Service name detection — maps ports to SSH, HTTP, MySQL, Redis, etc.
- Live streaming results — open ports print immediately as found
- `--only-open` flag to hide closed/filtered ports
- Zero dependencies — pure Python standard library

---

## Web UI

Open `index.html` in any browser. No install, no server needed.

```
1. Enter a target host
2. Pick a port preset or enter custom ports
3. Click "run scan"
```

> **Note:** Browsers can't make raw TCP connections, so the web UI uses HTTP fetch and WebSocket probing. For full TCP accuracy, use the CLI tool.

---

## CLI Tool

### Install

```bash
mv scan.py ~/.local/bin/scan
chmod +x ~/.local/bin/scan
```

Add to PATH if needed (add to `~/.bashrc` or `~/.zshrc`):

```bash
export PATH="$HOME/.local/bin:$PATH"
```

### Usage

```bash
# Scan top 100 common ports (default)
scan localhost

# Scan specific ports
scan 192.168.1.1 -p 22,80,443

# Scan a range
scan 192.168.1.1 -p 1-1024

# Full scan, fast
scan 192.168.1.1 -p 1-65535 --workers 500

# Only show open ports
scan example.com --only-open

# Custom timeout
scan 10.0.0.1 --timeout 2.0
```

### Options

| Flag | Default | Description |
|------|---------|-------------|
| `-p`, `--ports` | top 100 | Ports to scan: `80`, `22,80,443`, `1-1024` |
| `-w`, `--workers` | 100 | Max concurrent connections |
| `-t`, `--timeout` | 1.0s | Per-port timeout in seconds |
| `-o`, `--only-open` | off | Only show open ports |
| `-v`, `--verbose` | off | Show all ports as they complete |

### Example output

```
  scan  192.168.1.1  (192.168.1.1)
  ports: 22,80,443  ·  workers: 100  ·  timeout: 1.0s

  PORT      STATE         SERVICE
  ──────  ──────────  ────────────────────
  22        open          SSH
  80        open          HTTP
  443       filtered

  ──────────────────────────────────────────────
  2 open  1 filtered  0 closed  — 0.84s
```

---

## Port states

| State | Meaning |
|-------|---------|
| `open` | A service is actively listening on this port |
| `closed` | Port is reachable but nothing is running |
| `filtered` | A firewall is blocking the probe |

---

## Ethical use

Only scan hosts you **own** or have **explicit written permission** to scan. Unauthorized port scanning may be illegal in your country. Always test on `localhost` or your own machines first.

---

## Files

| File | Description |
|------|-------------|
| `index.html` | Web UI — open in any browser |
| `scan.py` | Python CLI tool |

---

## License

MIT — free to use, modify, and distribute.
