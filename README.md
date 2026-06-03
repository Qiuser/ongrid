# <img src="web/public/ongrid-logo.svg" alt="" width="40" align="absmiddle" style="vertical-align: middle;" /> Ongrid

> **An AI agent that knows your systems.** *Closes the loop between alert and answer — across metrics, logs, traces, and code.*

[![Go Report Card](https://goreportcard.com/badge/github.com/ongridio/ongrid)](https://goreportcard.com/report/github.com/ongridio/ongrid)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Tech](https://img.shields.io/badge/Tech-Go%20%7C%20TypeScript%20%7C%20React-blue)](#)

English | [简体中文](./README_ZH.md) | [日本語](./README_JA.md) | [한국어](./README_KO.md) | [Español](./README_ES.md) | [Français](./README_FR.md) | [Deutsch](./README_DE.md) | [Português](./README_PT.md) | [Русский](./README_RU.md)

[Install](#install) • [Features](#features) • [Integrations](#integrations) • [License](#license)

---

<p align="center">
  <img src="docs/assets/demo.gif" alt="Ongrid demo" width="100%" />
</p>

## Install

Download the latest release, extract it, and run the installer (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9):

```bash
# 1. Download latest release (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9)
wget https://github.com/ongridio/ongrid/releases/download/v0.7.167/ongrid-v0.7.167-linux-amd64.tar.xz

# 2. Extract
tar -xf ongrid-v0.7.167-linux-amd64.tar.xz && cd ongrid-v0.7.167-linux-amd64

# 3. Install
sudo ./install.sh
```

### Or run from source

Local dev: set the admin account + one model API key, then bring up the full stack.

```bash
cp deploy/.env.example deploy/.env
make compose-up    # make compose-down to stop
```

## Features

|   | Feature | Description |
|---|---|---|
| 🤖 | **Coordinator + Specialist two-tier agent** | The coordinator runs the conversation and dispatches to SRE / network / DB / asset specialist sub-agents, each with its own toolbag and persona. The UI locale is threaded end-to-end. |
| 🚨 | **Auto-investigate on alert** | An alert fires, the investigator spawns an RCA worker, follows the trail, and writes the root cause + evidence chain back to a chat session — runs whether you are on call or not. |
| 🔍 | **Root-cause RCA, not surface chat** | The agent walks the service topology for blast radius, correlates metrics / logs / traces, and pins the "why" down to a **source-code line**. |
| 🔒 | **Zero inbound ports** | The edge dials out; hosts open no port 22 / 80 / 443. The telemetry data plane is separated from the control plane. |
| 💻 | **Browser SSH** | A reverse-tunnel interactive shell into any host over the same outbound connection — no SSH keys to distribute, no jumpbox, no port 22. Every command audited. |
| 🐳 | **Self-hostable in one command** | `docker compose up` brings up the full stack (manager + MySQL + Qdrant + frontier). No SaaS dependency. |
| 📊 | **Full observability stack built in** | Prometheus (metrics), Loki (logs), Tempo (traces), Grafana (dashboards) wired up out of the box. Ask in natural language; the agent writes the PromQL / LogQL / TraceQL. |
| 🧠 | **Bring your own model** | Anthropic / OpenAI / GLM / DeepSeek / Gemini / Kimi or any OpenAI-compatible endpoint. Provider routing and default-model switching are hot — no restart. |
| 💬 | **Two-way IM channels** | Slack / Telegram / Larksuite (Feishu) / DingTalk / WeCom — ask from wherever your team already talks. Per-channel allow-list and per-channel locale. |
| 🛠️ | **Read-only host tools, every call audited** | bash (sandboxed), `host_probe_*`, `query_promql`, `expand_topology`, 26+ inspection tools. The viewer role automatically gets the ClassSafe-only subset. |

## Integrations

Drop-in for the observability, channel, and model stacks your team already uses.

| | |
|---|---|
| **Observability** | <img src="https://api.iconify.design/logos:prometheus.svg" alt="Prometheus" title="Prometheus" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:grafana.svg" alt="Grafana" title="Grafana" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/loki.svg" alt="Loki" title="Loki" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/tempo.svg" alt="Tempo" title="Tempo" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/opentelemetry.svg" alt="OpenTelemetry" title="OpenTelemetry" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:qdrant-icon.svg" alt="Qdrant" title="Qdrant" width="28" height="28" /> |
| **Channels** | <img src="https://api.iconify.design/logos:slack-icon.svg" alt="Slack" title="Slack" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:telegram.svg" alt="Telegram" title="Telegram" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/larksuite.svg" alt="Larksuite" title="Larksuite" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/dingtalk.svg" alt="DingTalk" title="DingTalk" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.simpleicons.org/wechat" alt="WeCom" title="WeCom" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:webhooks.svg" alt="Webhook" title="Webhook" width="28" height="28" /> |
| **Models** | <img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/claude-color.svg" alt="Anthropic" title="Anthropic" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/openai.svg" alt="OpenAI" title="OpenAI" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/gemini-color.svg" alt="Gemini" title="Gemini" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/deepseek-color.svg" alt="DeepSeek" title="DeepSeek" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/zhipu.svg" alt="Zhipu" title="Zhipu" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/kimi-color.svg" alt="Kimi" title="Kimi" width="28" height="28" /> |

## License

Apache 2.0 — see [LICENSE](LICENSE).
