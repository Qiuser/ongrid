# <img src="web/public/ongrid-logo.svg" alt="" width="40" align="absmiddle" style="vertical-align: middle;" /> Ongrid

> **Um agente de IA que conhece seus sistemas.** *Fecha o ciclo entre alerta e causa raiz —— através de métricas, logs, traces e código.*

[![Go Report Card](https://goreportcard.com/badge/github.com/ongridio/ongrid)](https://goreportcard.com/report/github.com/ongridio/ongrid)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Tech](https://img.shields.io/badge/Tech-Go%20%7C%20TypeScript%20%7C%20React-blue)](#)

[English](./README.md) | [简体中文](./README_ZH.md) | [日本語](./README_JA.md) | [한국어](./README_KO.md) | [Español](./README_ES.md) | [Français](./README_FR.md) | [Deutsch](./README_DE.md) | Português | [Русский](./README_RU.md)

[Instalação](#instalação) • [Recursos](#recursos) • [Integrações](#integrações) • [Licença](#licença)

---

<p align="center">
  <img src="docs/assets/demo.gif" alt="Ongrid demo" width="100%" />
</p>

## Instalação

Baixe a última release, descompacte e execute o instalador (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9):

```bash
# 1. Baixe a última release (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9)
wget https://github.com/ongridio/ongrid/releases/download/v0.7.167/ongrid-v0.7.167-linux-amd64.tar.xz

# 2. Descompactar
tar -xf ongrid-v0.7.167-linux-amd64.tar.xz && cd ongrid-v0.7.167-linux-amd64

# 3. Instalar
sudo ./install.sh
```

### Ou executar a partir do código

Desenvolvimento local: configure a conta admin e uma API key de modelo, depois suba todo o stack.

```bash
cp deploy/.env.example deploy/.env
make compose-up    # make compose-down to stop
```

## Recursos

|   | Feature | Description |
|---|---|---|
| 🤖 | **Agentes em dois níveis Coordinator + Specialist** | O coordinator gerencia a conversa e delega para sub-agentes SRE / rede / DB / ativos. Cada specialist tem seu próprio toolbag e persona; o locale da UI é propagado por toda a cadeia. |
| 🚨 | **Auto-investigação ao disparar alerta** | Alerta dispara → o investigator lança um RCA worker → causa raiz + cadeia de evidências reescritas na sessão de chat. Roda mesmo fora do horário de plantão. |
| 🔍 | **RCA de causa raiz, não conversa superficial** | O agente percorre a topologia de serviços para análise de raio de impacto, correlaciona métricas / logs / traces e identifica o "porquê" até uma **linha de código fonte**. |
| 🔒 | **Zero portas de entrada** | O edge disca para fora; os hosts não abrem nenhuma porta 22 / 80 / 443. O plano de dados de telemetria é separado do plano de controle. |
| 💻 | **SSH no navegador** | Um shell interativo para qualquer host pelo mesmo túnel de saída revertido. Sem distribuir chaves SSH, sem jumpbox, sem porta 22. Cada comando auditado. |
| 🐳 | **Self-host em um comando** | `docker compose up` sobe a stack completa (manager + MySQL + Qdrant + frontier). Zero dependência SaaS. |
| 📊 | **Stack de observabilidade integrada** | Prometheus (métricas) / Loki (logs) / Tempo (traces) / Grafana (dashboards) prontos automaticamente. Pergunte em linguagem natural e o agente escreve PromQL / LogQL / TraceQL. |
| 🧠 | **Traga seu próprio modelo** | Anthropic / OpenAI / GLM / DeepSeek / Gemini / Kimi ou qualquer endpoint compatível com OpenAI. Roteamento de provedores e troca de modelo padrão a quente, sem reiniciar. |
| 💬 | **Canais IM bidirecionais** | Slack / Telegram / Larksuite (Feishu) / DingTalk / WeCom — pergunte de onde sua equipe já conversa; allow-list por canal e idioma por canal. |
| 🛠️ | **Ferramentas de host só-leitura, cada chamada auditada** | bash (sandbox), `host_probe_*`, `query_promql`, `expand_topology`, 26+ ferramentas. O papel viewer recebe automaticamente apenas o subconjunto ClassSafe. |

## Integrações

Drop-in para os stacks de observabilidade, canais e modelos que sua equipe já usa.

| | |
|---|---|
| **Observabilidade** | <img src="https://api.iconify.design/logos:prometheus.svg" alt="Prometheus" title="Prometheus" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:grafana.svg" alt="Grafana" title="Grafana" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/loki.svg" alt="Loki" title="Loki" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/tempo.svg" alt="Tempo" title="Tempo" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/opentelemetry.svg" alt="OpenTelemetry" title="OpenTelemetry" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:qdrant-icon.svg" alt="Qdrant" title="Qdrant" width="28" height="28" /> |
| **Canais** | <img src="https://api.iconify.design/logos:slack-icon.svg" alt="Slack" title="Slack" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:telegram.svg" alt="Telegram" title="Telegram" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/larksuite.svg" alt="Larksuite" title="Larksuite" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/dingtalk.svg" alt="DingTalk" title="DingTalk" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.simpleicons.org/wechat" alt="WeCom" title="WeCom" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:webhooks.svg" alt="Webhook" title="Webhook" width="28" height="28" /> |
| **Modelos** | <img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/claude-color.svg" alt="Anthropic" title="Anthropic" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/openai.svg" alt="OpenAI" title="OpenAI" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/gemini-color.svg" alt="Gemini" title="Gemini" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/deepseek-color.svg" alt="DeepSeek" title="DeepSeek" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/zhipu.svg" alt="Zhipu" title="Zhipu" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/kimi-color.svg" alt="Kimi" title="Kimi" width="28" height="28" /> |

## Licença

Apache 2.0 — veja [LICENSE](LICENSE).
