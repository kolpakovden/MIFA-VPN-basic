# MIFA-VPN

Production-ready modular installer for Xray (VLESS + Reality).

MIFA-VPN is a structured, open-source deployment toolkit built around Xray-core.  
It provides a clean installation lifecycle, modular architecture and production-grade setup flow.

---

## Features

- Modular installer (`--core`, `--monitoring`, `--bot`)
- Idempotent installation
- Upgrade & uninstall support
- Auto-generation of UUID and Reality keys
- Structured repository layout
- Production-oriented design
- Ready for automation & CI

---

## What It Installs

Core module installs:

- Xray (VLESS + Reality)
- Systemd service
- Auto-generated secure config
- Proper directory structure

Optional modules:

- Monitoring stack (placeholder)
- Automation bot (placeholder)

---

## 🏗 Architecture

Client
↓
Internet
↓
VLESS + Reality (TCP 443)
↓
Xray
↓
Freedom outbound

---

## Quick Start

### Clone repository

```bash
git clone https://github.com/yourname/MIFA-VPN.git
cd MIFA-VPN

### Install everything
sudo ./cmd/install.sh --all

Or install only core:

sudo ./cmd/install.sh --core

---

| Command        | Description                 |
| -------------- | --------------------------- |
| `--core`       | Install Xray core           |
| `--monitoring` | Install monitoring module   |
| `--bot`        | Install automation bot      |
| `--all`        | Install everything          |
| `--upgrade`    | Upgrade Xray                |
| `--uninstall`  | Remove installed components |

---

## Directory Structure

cmd/            → CLI entrypoint
internal/       → Installer modules
core/           → Xray templates
monitoring/     → Monitoring stack
automation/     → Bot & automation
docs/           → Documentation
security/       → Security hardening

---

## Security Model

Reality transport enabled
Private key generated on server
UUID per client
Config permissions 640
Systemd integration
For full hardening guide see:

security/security-hardening.md

---

## Production Notes

---

Requires systemd-based Linux (Ubuntu/Debian recommended)
Port 443 must be free
Run as root
Monitoring module is optional
Designed for VPS deployment

---

## Upgrade
sudo ./cmd/install.sh --upgrade

---

## Uninstall
sudo ./cmd/install.sh --uninstall

---

## License
MIT License

---

---

#  Текущее состояние проекта

| Компонент | Статус |
|------------|--------|
| Структура | ✅ |
| Installer | ✅ |
| Lifecycle | ✅ |
| OSS-ready | ✅ |
| README | ✅ после обновления |
| CI | ❌ (следующий шаг) |
| Docker | ❌ |
| Multi-user | ❌ |

---

