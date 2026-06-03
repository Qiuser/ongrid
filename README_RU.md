# <img src="web/public/ongrid-logo.svg" alt="" width="40" align="absmiddle" style="vertical-align: middle;" /> Ongrid

> **AI-агент, который знает ваши системы.** *Замыкает цикл от алерта до первопричины —— по метрикам, логам, трейсам и коду.*

[![Go Report Card](https://goreportcard.com/badge/github.com/ongridio/ongrid)](https://goreportcard.com/report/github.com/ongridio/ongrid)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Tech](https://img.shields.io/badge/Tech-Go%20%7C%20TypeScript%20%7C%20React-blue)](#)

[English](./README.md) | [简体中文](./README_ZH.md) | [日本語](./README_JA.md) | [한국어](./README_KO.md) | [Español](./README_ES.md) | [Français](./README_FR.md) | [Deutsch](./README_DE.md) | [Português](./README_PT.md) | Русский

[Установка](#установка) • [Возможности](#возможности) • [Интеграции](#интеграции) • [Лицензия](#лицензия)

---

<p align="center">
  <img src="docs/assets/demo.gif" alt="Ongrid demo" width="100%" />
</p>

## Установка

Скачайте последний релиз, распакуйте и запустите скрипт установки (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9):

```bash
# 1. Скачайте последний релиз (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9)
wget https://github.com/ongridio/ongrid/releases/download/v0.7.167/ongrid-v0.7.167-linux-amd64.tar.xz

# 2. Распаковка
tar -xf ongrid-v0.7.167-linux-amd64.tar.xz && cd ongrid-v0.7.167-linux-amd64

# 3. Установка
sudo ./install.sh
```

### Или запустить из исходников

Локальная разработка: настройте админ-аккаунт и API-ключ модели, затем поднимите весь стек.

```bash
cp deploy/.env.example deploy/.env
make compose-up    # make compose-down to stop
```

## Возможности

|   | Feature | Description |
|---|---|---|
| 🤖 | **Двухуровневые агенты Coordinator + Specialist** | Coordinator ведёт диалог и распределяет задачи между специализированными суб-агентами SRE / сеть / БД / активы. У каждого specialist своя toolbag и persona; UI-локаль пробрасывается через всю цепочку. |
| 🚨 | **Авто-исследование при срабатывании алерта** | Алерт срабатывает → investigator запускает RCA-worker → корневая причина + цепочка доказательств записываются обратно в чат. Работает и в нерабочее время. |
| 🔍 | **Корневая RCA, а не поверхностный диалог** | Агент обходит топологию сервисов для анализа радиуса поражения, коррелирует метрики / логи / трейсы и определяет «почему» вплоть до **строки исходного кода**. |
| 🔒 | **Ноль входящих портов** | edge выходит наружу; хосты не открывают порты 22 / 80 / 443. Плоскость данных телеметрии отделена от плоскости управления. |
| 💻 | **SSH в браузере** | Интерактивная оболочка до любого хоста через тот же исходящий туннель обратно. Не нужно распространять SSH-ключи, не нужны jumpbox и порт 22. Каждая команда в аудите. |
| 🐳 | **Self-host одной командой** | `docker compose up` поднимает весь стек (manager + MySQL + Qdrant + frontier). Никакой SaaS-зависимости. |
| 📊 | **Стек observability встроен** | Prometheus (метрики) / Loki (логи) / Tempo (трейсы) / Grafana (дашборды) разворачиваются автоматически. Задавайте вопрос на естественном языке — агент напишет PromQL / LogQL / TraceQL. |
| 🧠 | **Принесите свою модель** | Anthropic / OpenAI / GLM / DeepSeek / Gemini / Kimi или любой OpenAI-совместимый эндпоинт. Маршрутизация провайдеров и смена дефолтной модели на лету, без перезапуска. |
| 💬 | **Двусторонние IM-каналы** | Slack / Telegram / Larksuite (Feishu) / DingTalk / WeCom — спрашивайте оттуда, где команда уже общается; allow-list на канал и локаль на канал. |
| 🛠️ | **Read-only host-инструменты, каждый вызов в аудите** | bash (sandbox), `host_probe_*`, `query_promql`, `expand_topology`, 26+ инструментов. Viewer-роль автоматически получает только ClassSafe-подмножество. |

## Интеграции

Подключается к стекам observability, каналов и моделей, которые ваша команда уже использует.

| | |
|---|---|
| **Observability** | <img src="https://api.iconify.design/logos:prometheus.svg" alt="Prometheus" title="Prometheus" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:grafana.svg" alt="Grafana" title="Grafana" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/loki.svg" alt="Loki" title="Loki" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/tempo.svg" alt="Tempo" title="Tempo" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/opentelemetry.svg" alt="OpenTelemetry" title="OpenTelemetry" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:qdrant-icon.svg" alt="Qdrant" title="Qdrant" width="28" height="28" /> |
| **Каналы** | <img src="https://api.iconify.design/logos:slack-icon.svg" alt="Slack" title="Slack" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:telegram.svg" alt="Telegram" title="Telegram" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/larksuite.svg" alt="Larksuite" title="Larksuite" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/dingtalk.svg" alt="DingTalk" title="DingTalk" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.simpleicons.org/wechat" alt="WeCom" title="WeCom" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:webhooks.svg" alt="Webhook" title="Webhook" width="28" height="28" /> |
| **Модели** | <img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/claude-color.svg" alt="Anthropic" title="Anthropic" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/openai.svg" alt="OpenAI" title="OpenAI" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/gemini-color.svg" alt="Gemini" title="Gemini" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/deepseek-color.svg" alt="DeepSeek" title="DeepSeek" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/zhipu.svg" alt="Zhipu" title="Zhipu" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/kimi-color.svg" alt="Kimi" title="Kimi" width="28" height="28" /> |

## Лицензия

Apache 2.0 — см. [LICENSE](LICENSE).
