# <img src="web/public/ongrid-logo.svg" alt="" width="40" align="absmiddle" style="vertical-align: middle;" /> Ongrid

> **懂你系统的 AI 运维 Agent。** *把告警和根因接起来 —— 跨指标、日志、链路和源码。*

[![Go Report Card](https://goreportcard.com/badge/github.com/ongridio/ongrid)](https://goreportcard.com/report/github.com/ongridio/ongrid)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Tech](https://img.shields.io/badge/Tech-Go%20%7C%20TypeScript%20%7C%20React-blue)](#)

[English](./README.md) | 简体中文 | [日本語](./README_JA.md) | [한국어](./README_KO.md) | [Español](./README_ES.md) | [Français](./README_FR.md) | [Deutsch](./README_DE.md) | [Português](./README_PT.md) | [Русский](./README_RU.md)

[安装](#安装) • [特性](#特性) • [集成](#集成) • [许可证](#许可证)

---

<p align="center">
  <img src="docs/assets/demo.gif" alt="Ongrid demo" width="100%" />
</p>

## 安装

下载最新 release，解压后运行安装脚本（Ubuntu 22.04+、Debian 12+、RHEL/Rocky 9）：

```bash
# 1. 下载最新 release（Ubuntu 22.04+、Debian 12+、RHEL/Rocky 9）
wget https://github.com/ongridio/ongrid/releases/download/v0.7.167/ongrid-v0.7.167-linux-amd64.tar.xz

# 2. 解压
tar -xf ongrid-v0.7.167-linux-amd64.tar.xz && cd ongrid-v0.7.167-linux-amd64

# 3. 安装
sudo ./install.sh
```

### 或从源码运行

本地开发：先配好管理员账号和一个模型 API key，再起整套栈。

```bash
cp deploy/.env.example deploy/.env
make compose-up    # make compose-down to stop
```

## 特性

|   | Feature | Description |
|---|---|---|
| 🤖 | **Coordinator + Specialist 双层 Agent** | coordinator 接对话和派活，按领域路由到 SRE / 网络 / DB / 资产 specialist 子 agent，各自独立 toolbag 和 persona；UI locale 全链贯穿。 |
| 🚨 | **告警触发自动调查** | 告警起飞 → investigator 自动派 RCA worker → 根因 + 证据链回填到聊天会话，没人值班也会跑。 |
| 🔍 | **根因 RCA，不是表面问答** | Agent 沿业务拓扑做爆炸半径分析、跨指标 / 日志 / 链路相关，定位**源码行**给出"为什么"。 |
| 🔒 | **零入站端口** | edge 主动外联，host 不开 22 / 80 / 443 任何端口；遥测数据面与控制面分离。 |
| 💻 | **浏览器 SSH** | 走同一条出站隧道反向打通，UI 内拿到目标主机交互式 shell；不用 SSH key / 跳板机 / 开 22；全程审计。 |
| 🐳 | **一行命令自托管整套栈** | `docker compose up` 起 manager + MySQL + Qdrant + frontier，零 SaaS 依赖。 |
| 📊 | **可观测全栈内置** | Prometheus 指标 / Loki 日志 / Tempo 链路 / Grafana 看板 自动起；自然语言提问，Agent 自动写 PromQL / LogQL / TraceQL。 |
| 🧠 | **自带任意模型** | Anthropic / OpenAI / GLM / DeepSeek / Gemini / Kimi 或任意 OpenAI 兼容端点；provider 路由 + default-model 热切换不用重启。 |
| 💬 | **双向 IM 通道** | Slack / Telegram / Larksuite (飞书) / DingTalk / WeCom，团队在哪聊就在哪发问；按通道 allow-list + 按通道语言。 |
| 🛠️ | **只读主机巡检工具 + 审计** | bash 沙箱、`host_probe_*`、`query_promql`、`expand_topology` 等 26+ 工具；viewer 角色只看 ClassSafe 工具。 |

## 集成

即插即用，对接团队现有的可观测、IM 通道与模型栈。

| | |
|---|---|
| **可观测** | <img src="https://api.iconify.design/logos:prometheus.svg" alt="Prometheus" title="Prometheus" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:grafana.svg" alt="Grafana" title="Grafana" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/loki.svg" alt="Loki" title="Loki" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/tempo.svg" alt="Tempo" title="Tempo" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/opentelemetry.svg" alt="OpenTelemetry" title="OpenTelemetry" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:qdrant-icon.svg" alt="Qdrant" title="Qdrant" width="28" height="28" /> |
| **通道** | <img src="https://api.iconify.design/logos:slack-icon.svg" alt="Slack" title="Slack" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:telegram.svg" alt="Telegram" title="Telegram" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/larksuite.svg" alt="Larksuite" title="Larksuite" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/dingtalk.svg" alt="DingTalk" title="DingTalk" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.simpleicons.org/wechat" alt="WeCom" title="WeCom" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:webhooks.svg" alt="Webhook" title="Webhook" width="28" height="28" /> |
| **模型** | <img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/claude-color.svg" alt="Anthropic" title="Anthropic" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/openai.svg" alt="OpenAI" title="OpenAI" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/gemini-color.svg" alt="Gemini" title="Gemini" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/deepseek-color.svg" alt="DeepSeek" title="DeepSeek" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/zhipu.svg" alt="Zhipu" title="Zhipu" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/kimi-color.svg" alt="Kimi" title="Kimi" width="28" height="28" /> |

## 许可证

Apache 2.0 — 见 [LICENSE](LICENSE)。
