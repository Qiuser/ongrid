# <img src="web/public/ongrid-logo.svg" alt="" width="40" align="absmiddle" style="vertical-align: middle;" /> Ongrid

> **Un agent IA qui connaît vos systèmes.** *Boucle la boucle entre alerte et cause racine —— à travers métriques, logs, traces et code.*

[![Go Report Card](https://goreportcard.com/badge/github.com/ongridio/ongrid)](https://goreportcard.com/report/github.com/ongridio/ongrid)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Tech](https://img.shields.io/badge/Tech-Go%20%7C%20TypeScript%20%7C%20React-blue)](#)

[English](./README.md) | [简体中文](./README_ZH.md) | [日本語](./README_JA.md) | [한국어](./README_KO.md) | [Español](./README_ES.md) | Français | [Deutsch](./README_DE.md) | [Português](./README_PT.md) | [Русский](./README_RU.md)

[Installation](#installation) • [Fonctionnalités](#fonctionnalités) • [Intégrations](#intégrations) • [Licence](#licence)

---

<p align="center">
  <img src="docs/assets/demo.gif" alt="Ongrid demo" width="100%" />
</p>

## Installation

Téléchargez la dernière release, décompressez-la et exécutez le script d’installation (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9) :

```bash
# 1. Téléchargez la dernière release (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9)
wget https://github.com/ongridio/ongrid/releases/download/v0.7.167/ongrid-v0.7.167-linux-amd64.tar.xz

# 2. Décompresser
tar -xf ongrid-v0.7.167-linux-amd64.tar.xz && cd ongrid-v0.7.167-linux-amd64

# 3. Installer
sudo ./install.sh
```

### Ou exécuter depuis les sources

Dev local : configurez le compte admin et une clé API de modèle, puis lancez la stack complète.

```bash
cp deploy/.env.example deploy/.env
make compose-up    # make compose-down to stop
```

## Fonctionnalités

|   | Feature | Description |
|---|---|---|
| 🤖 | **Agents à deux étages Coordinator + Specialist** | Le coordinator gère la conversation et délègue aux sous-agents SRE / réseau / DB / actifs. Chaque specialist a son propre toolbag et persona ; la locale UI est propagée tout au long de la chaîne. |
| 🚨 | **Investigation automatique sur alerte** | L’alerte se déclenche → l’investigator lance un RCA worker → cause racine + chaîne d’éléments de preuve réécrits dans la session de chat. Tourne même en dehors des heures d’astreinte. |
| 🔍 | **RCA cause racine, pas une simple conversation** | L’agent parcourt la topologie des services pour analyser le rayon d’impact, corrèle métriques / logs / traces et identifie le "pourquoi" jusqu’à une **ligne de code source**. |
| 🔒 | **Zéro port entrant** | L’edge compose vers l’extérieur ; les hôtes n’ouvrent aucun port 22 / 80 / 443. Le plan de données télémétrie est séparé du plan de contrôle. |
| 💻 | **SSH dans le navigateur** | Un shell interactif vers n’importe quel hôte via le même tunnel sortant inversé. Pas de clé SSH à distribuer, pas de jumpbox, pas de port 22. Chaque commande auditée. |
| 🐳 | **Auto-hébergeable en une commande** | `docker compose up` lance la stack complète (manager + MySQL + Qdrant + frontier). Zéro dépendance SaaS. |
| 📊 | **Stack d’observabilité intégrée** | Prometheus (métriques) / Loki (logs) / Tempo (traces) / Grafana (tableaux de bord) déployés automatiquement. Posez la question en langage naturel, l’agent rédige le PromQL / LogQL / TraceQL. |
| 🧠 | **Apportez votre modèle** | Anthropic / OpenAI / GLM / DeepSeek / Gemini / Kimi ou tout endpoint compatible OpenAI. Routage des fournisseurs et changement du modèle par défaut à chaud, sans redémarrage. |
| 💬 | **Canaux IM bidirectionnels** | Slack / Telegram / Larksuite (Feishu) / DingTalk / WeCom — posez vos questions là où votre équipe parle déjà ; allow-list par canal et langue par canal. |
| 🛠️ | **Outils host en lecture seule, chaque appel audité** | bash (sandbox), `host_probe_*`, `query_promql`, `expand_topology`, 26+ outils. Le rôle viewer obtient automatiquement le sous-ensemble ClassSafe. |

## Intégrations

S’intègre aux stacks d’observabilité, de canaux et de modèles déjà en place.

| | |
|---|---|
| **Observabilité** | <img src="https://api.iconify.design/logos:prometheus.svg" alt="Prometheus" title="Prometheus" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:grafana.svg" alt="Grafana" title="Grafana" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/loki.svg" alt="Loki" title="Loki" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/tempo.svg" alt="Tempo" title="Tempo" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/opentelemetry.svg" alt="OpenTelemetry" title="OpenTelemetry" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:qdrant-icon.svg" alt="Qdrant" title="Qdrant" width="28" height="28" /> |
| **Canaux** | <img src="https://api.iconify.design/logos:slack-icon.svg" alt="Slack" title="Slack" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:telegram.svg" alt="Telegram" title="Telegram" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/larksuite.svg" alt="Larksuite" title="Larksuite" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/dingtalk.svg" alt="DingTalk" title="DingTalk" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.simpleicons.org/wechat" alt="WeCom" title="WeCom" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:webhooks.svg" alt="Webhook" title="Webhook" width="28" height="28" /> |
| **Modèles** | <img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/claude-color.svg" alt="Anthropic" title="Anthropic" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/openai.svg" alt="OpenAI" title="OpenAI" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/gemini-color.svg" alt="Gemini" title="Gemini" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/deepseek-color.svg" alt="DeepSeek" title="DeepSeek" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/zhipu.svg" alt="Zhipu" title="Zhipu" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/kimi-color.svg" alt="Kimi" title="Kimi" width="28" height="28" /> |

## Licence

Apache 2.0 — voir [LICENSE](LICENSE).
