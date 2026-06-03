# <img src="web/public/ongrid-logo.svg" alt="" width="40" align="absmiddle" style="vertical-align: middle;" /> Ongrid

> **Un agente de IA que conoce tus sistemas.** *Cierra el bucle entre alerta y causa raíz —— a través de métricas, logs, trazas y código.*

[![Go Report Card](https://goreportcard.com/badge/github.com/ongridio/ongrid)](https://goreportcard.com/report/github.com/ongridio/ongrid)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Tech](https://img.shields.io/badge/Tech-Go%20%7C%20TypeScript%20%7C%20React-blue)](#)

[English](./README.md) | [简体中文](./README_ZH.md) | [日本語](./README_JA.md) | [한국어](./README_KO.md) | Español | [Français](./README_FR.md) | [Deutsch](./README_DE.md) | [Português](./README_PT.md) | [Русский](./README_RU.md)

[Instalación](#instalación) • [Características](#características) • [Integraciones](#integraciones) • [Licencia](#licencia)

---

<p align="center">
  <img src="docs/assets/demo.gif" alt="Ongrid demo" width="100%" />
</p>

## Instalación

Descarga la última release, descomprímela y ejecuta el instalador (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9):

```bash
# 1. Descarga la última release (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9)
wget https://github.com/ongridio/ongrid/releases/download/v0.7.167/ongrid-v0.7.167-linux-amd64.tar.xz

# 2. Descomprimir
tar -xf ongrid-v0.7.167-linux-amd64.tar.xz && cd ongrid-v0.7.167-linux-amd64

# 3. Instalar
sudo ./install.sh
```

### O ejecutar desde el código fuente

Desarrollo local: configura la cuenta de admin y una API key de modelo, y levanta todo el stack.

```bash
cp deploy/.env.example deploy/.env
make compose-up    # make compose-down to stop
```

## Características

|   | Feature | Description |
|---|---|---|
| 🤖 | **Agentes en dos niveles Coordinator + Specialist** | El coordinator gestiona la conversación y delega a sub-agentes SRE / red / DB / activos. Cada specialist tiene su propio toolbag y persona; la locale de UI se propaga por toda la cadena. |
| 🚨 | **Auto-investigación al disparar alerta** | La alerta dispara → el investigator lanza un RCA worker → causa raíz + cadena de evidencias se escriben de vuelta en la sesión de chat. Se ejecuta aunque no haya nadie de guardia. |
| 🔍 | **RCA de causa raíz, no charla superficial** | El agente recorre la topología de servicios para analizar el radio de impacto, correlaciona métricas / logs / trazas y precisa el "por qué" hasta una **línea de código fuente**. |
| 🔒 | **Cero puertos entrantes** | El edge sale al exterior; los hosts no abren ningún puerto 22 / 80 / 443. El plano de datos de telemetría está separado del plano de control. |
| 💻 | **SSH en el navegador** | Un shell interactivo a cualquier host a través del mismo túnel saliente revertido. Sin distribuir claves SSH, sin jumpbox, sin puerto 22. Cada comando auditado. |
| 🐳 | **Autoalojable en un comando** | `docker compose up` levanta toda la stack (manager + MySQL + Qdrant + frontier). Cero dependencia SaaS. |
| 📊 | **Stack de observabilidad integrada** | Prometheus (métricas) / Loki (logs) / Tempo (trazas) / Grafana (dashboards) listos automáticamente. Pregunta en lenguaje natural y el agente escribe el PromQL / LogQL / TraceQL. |
| 🧠 | **Trae tu propio modelo** | Anthropic / OpenAI / GLM / DeepSeek / Gemini / Kimi o cualquier endpoint compatible con OpenAI. El enrutamiento de proveedores y el cambio de modelo por defecto son en caliente, sin reinicio. |
| 💬 | **Canales IM bidireccionales** | Slack / Telegram / Larksuite (Feishu) / DingTalk / WeCom — pregunta desde donde tu equipo ya habla; allow-list por canal y idioma por canal. |
| 🛠️ | **Herramientas de host de solo lectura, cada llamada auditada** | bash (sandbox), `host_probe_*`, `query_promql`, `expand_topology`, 26+ herramientas. El rol viewer obtiene automáticamente solo el subconjunto ClassSafe. |

## Integraciones

Se integra con los stacks de observabilidad, canales y modelos que tu equipo ya usa.

| | |
|---|---|
| **Observabilidad** | <img src="https://api.iconify.design/logos:prometheus.svg" alt="Prometheus" title="Prometheus" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:grafana.svg" alt="Grafana" title="Grafana" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/loki.svg" alt="Loki" title="Loki" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/tempo.svg" alt="Tempo" title="Tempo" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/opentelemetry.svg" alt="OpenTelemetry" title="OpenTelemetry" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:qdrant-icon.svg" alt="Qdrant" title="Qdrant" width="28" height="28" /> |
| **Canales** | <img src="https://api.iconify.design/logos:slack-icon.svg" alt="Slack" title="Slack" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:telegram.svg" alt="Telegram" title="Telegram" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/larksuite.svg" alt="Larksuite" title="Larksuite" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/dingtalk.svg" alt="DingTalk" title="DingTalk" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.simpleicons.org/wechat" alt="WeCom" title="WeCom" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:webhooks.svg" alt="Webhook" title="Webhook" width="28" height="28" /> |
| **Modelos** | <img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/claude-color.svg" alt="Anthropic" title="Anthropic" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/openai.svg" alt="OpenAI" title="OpenAI" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/gemini-color.svg" alt="Gemini" title="Gemini" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/deepseek-color.svg" alt="DeepSeek" title="DeepSeek" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/zhipu.svg" alt="Zhipu" title="Zhipu" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/kimi-color.svg" alt="Kimi" title="Kimi" width="28" height="28" /> |

## Licencia

Apache 2.0 — ver [LICENSE](LICENSE).
