# <img src="web/public/ongrid-logo.svg" alt="" width="40" align="absmiddle" style="vertical-align: middle;" /> Ongrid

> **Ein KI-Agent, der Ihre Systeme kennt.** *Schließt den Kreis zwischen Alarm und Ursache —— über Metriken, Logs, Traces und Code hinweg.*

[![Go Report Card](https://goreportcard.com/badge/github.com/ongridio/ongrid)](https://goreportcard.com/report/github.com/ongridio/ongrid)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Tech](https://img.shields.io/badge/Tech-Go%20%7C%20TypeScript%20%7C%20React-blue)](#)

[English](./README.md) | [简体中文](./README_ZH.md) | [日本語](./README_JA.md) | [한국어](./README_KO.md) | [Español](./README_ES.md) | [Français](./README_FR.md) | Deutsch | [Português](./README_PT.md) | [Русский](./README_RU.md)

[Installation](#installation) • [Funktionen](#funktionen) • [Integrationen](#integrationen) • [Lizenz](#lizenz)

---

<p align="center">
  <img src="docs/assets/demo.gif" alt="Ongrid demo" width="100%" />
</p>

## Installation

Laden Sie das aktuelle Release herunter, entpacken Sie es und führen Sie das Installationsskript aus (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9):

```bash
# 1. Aktuelles Release herunterladen (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9)
wget https://github.com/ongridio/ongrid/releases/download/v0.7.167/ongrid-v0.7.167-linux-amd64.tar.xz

# 2. Entpacken
tar -xf ongrid-v0.7.167-linux-amd64.tar.xz && cd ongrid-v0.7.167-linux-amd64

# 3. Installieren
sudo ./install.sh
```

### Oder aus dem Quellcode ausführen

Lokale Entwicklung: Admin-Konto und einen Modell-API-Key konfigurieren, dann die gesamte Stack starten.

```bash
cp deploy/.env.example deploy/.env
make compose-up    # make compose-down to stop
```

## Funktionen

|   | Feature | Description |
|---|---|---|
| 🤖 | **Coordinator + Specialist Zweischicht-Agent** | Der Coordinator führt das Gespräch und verteilt an Sub-Agenten SRE / Netzwerk / DB / Asset. Jeder Specialist hat eine eigene Toolbag und Persona; die UI-Sprache wird durch die gesamte Kette geleitet. |
| 🚨 | **Auto-Investigation bei Alarm** | Alarm löst aus → der Investigator startet einen RCA-Worker → Grundursache + Beweisketten werden in die Chat-Session zurückgeschrieben. Läuft auch außerhalb der Bereitschaft. |
| 🔍 | **Grundursache-RCA, kein Oberflächengespräch** | Der Agent geht die Service-Topologie für den Blast Radius durch, korreliert Metriken / Logs / Traces und schließt das "Warum" bis zu einer **Quellcode-Zeile** ein. |
| 🔒 | **Null eingehende Ports** | Der Edge wählt nach außen; Hosts öffnen kein Port 22 / 80 / 443. Telemetrie-Datenebene ist von der Steuerungsebene getrennt. |
| 💻 | **SSH im Browser** | Eine interaktive Shell zu jedem Host über denselben ausgehenden Tunnel rückwärts. Keine SSH-Schlüssel verteilen, kein Jumpbox, kein Port 22. Jeder Befehl auditiert. |
| 🐳 | **Selbst-gehostet in einem Befehl** | `docker compose up` startet die gesamte Stack (manager + MySQL + Qdrant + frontier). Null SaaS-Abhängigkeit. |
| 📊 | **Vollständiger Observability-Stack integriert** | Prometheus (Metriken) / Loki (Logs) / Tempo (Traces) / Grafana (Dashboards) werden automatisch bereitgestellt. Fragen Sie in natürlicher Sprache, der Agent schreibt PromQL / LogQL / TraceQL. |
| 🧠 | **Eigenes Modell mitbringen** | Anthropic / OpenAI / GLM / DeepSeek / Gemini / Kimi oder jeder OpenAI-kompatible Endpunkt. Provider-Routing und Standardmodell-Wechsel im Betrieb, ohne Neustart. |
| 💬 | **Zweiwege-IM-Kanäle** | Slack / Telegram / Larksuite (Feishu) / DingTalk / WeCom — fragen Sie dort, wo Ihr Team bereits spricht; Allow-list pro Kanal und Sprache pro Kanal. |
| 🛠️ | **Schreibgeschützte Host-Tools, jeder Aufruf auditiert** | bash (Sandbox), `host_probe_*`, `query_promql`, `expand_topology`, 26+ Tools. Die Viewer-Rolle erhält automatisch nur das ClassSafe-Subset. |

## Integrationen

Drop-in für die Observability-, Channel- und Modell-Stacks, die Ihr Team bereits nutzt.

| | |
|---|---|
| **Observability** | <img src="https://api.iconify.design/logos:prometheus.svg" alt="Prometheus" title="Prometheus" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:grafana.svg" alt="Grafana" title="Grafana" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/loki.svg" alt="Loki" title="Loki" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/tempo.svg" alt="Tempo" title="Tempo" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/opentelemetry.svg" alt="OpenTelemetry" title="OpenTelemetry" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:qdrant-icon.svg" alt="Qdrant" title="Qdrant" width="28" height="28" /> |
| **Kanäle** | <img src="https://api.iconify.design/logos:slack-icon.svg" alt="Slack" title="Slack" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:telegram.svg" alt="Telegram" title="Telegram" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/larksuite.svg" alt="Larksuite" title="Larksuite" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/dingtalk.svg" alt="DingTalk" title="DingTalk" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.simpleicons.org/wechat" alt="WeCom" title="WeCom" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:webhooks.svg" alt="Webhook" title="Webhook" width="28" height="28" /> |
| **Modelle** | <img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/claude-color.svg" alt="Anthropic" title="Anthropic" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/openai.svg" alt="OpenAI" title="OpenAI" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/gemini-color.svg" alt="Gemini" title="Gemini" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/deepseek-color.svg" alt="DeepSeek" title="DeepSeek" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/zhipu.svg" alt="Zhipu" title="Zhipu" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/kimi-color.svg" alt="Kimi" title="Kimi" width="28" height="28" /> |

## Lizenz

Apache 2.0 — siehe [LICENSE](LICENSE).
