# <img src="web/public/ongrid-logo.svg" alt="" width="40" align="absmiddle" style="vertical-align: middle;" /> Ongrid

> **시스템을 이해하는 운영 AI 에이전트.** *알림과 근본 원인을 잇다 —— 메트릭, 로그, 트레이스, 소스 코드 전반에 걸쳐.*

[![Go Report Card](https://goreportcard.com/badge/github.com/ongridio/ongrid)](https://goreportcard.com/report/github.com/ongridio/ongrid)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Tech](https://img.shields.io/badge/Tech-Go%20%7C%20TypeScript%20%7C%20React-blue)](#)

[English](./README.md) | [简体中文](./README_ZH.md) | [日本語](./README_JA.md) | 한국어 | [Español](./README_ES.md) | [Français](./README_FR.md) | [Deutsch](./README_DE.md) | [Português](./README_PT.md) | [Русский](./README_RU.md)

[설치](#설치) • [기능](#기능) • [연동](#연동) • [라이선스](#라이선스)

---

<p align="center">
  <img src="docs/assets/demo.gif" alt="Ongrid demo" width="100%" />
</p>

## 설치

최신 릴리스를 다운로드하고 압축을 푼 다음 설치 스크립트를 실행하세요 (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9):

```bash
# 1. 최신 릴리스 다운로드 (Ubuntu 22.04+, Debian 12+, RHEL/Rocky 9)
wget https://github.com/ongridio/ongrid/releases/download/v0.7.167/ongrid-v0.7.167-linux-amd64.tar.xz

# 2. 압축 해제
tar -xf ongrid-v0.7.167-linux-amd64.tar.xz && cd ongrid-v0.7.167-linux-amd64

# 3. 설치
sudo ./install.sh
```

### 또는 소스에서 실행

로컬 개발: 관리자 계정과 모델 API 키를 설정한 후 전체 스택을 기동합니다.

```bash
cp deploy/.env.example deploy/.env
make compose-up    # make compose-down to stop
```

## 기능

|   | Feature | Description |
|---|---|---|
| 🤖 | **Coordinator + Specialist 이중 에이전트** | coordinator가 대화와 작업 배정을 맡고, SRE / 네트워크 / DB / 자산 specialist 서브 에이전트로 라우팅. 각 specialist는 독립 toolbag와 persona, UI 로케일은 전체 체인에 전달. |
| 🚨 | **알림 발생 시 자동 조사** | 알림 발생 → investigator가 RCA worker 파견 → 근본 원인 + 증거 체인을 채팅 세션에 기록. 당직자가 없어도 실행. |
| 🔍 | **근본 원인 RCA, 표면 대화가 아님** | Agent가 서비스 토폴로지로 영향 범위를 분석하고, 메트릭 / 로그 / 트레이스를 상관 분석하여 "왜"를 **소스 코드 라인**까지 특정. |
| 🔒 | **인바운드 포트 0** | edge가 외부로 발신; 호스트는 22 / 80 / 443 어떤 포트도 열지 않음. 텔레메트리 데이터 플레인은 컨트롤 플레인과 분리. |
| 💻 | **브라우저 SSH** | 같은 아웃바운드 터널을 역방향으로 열어 UI에서 대상 호스트의 대화형 셸로. SSH 키 배포 / 점프 호스트 / 포트 22 모두 불필요. 모든 명령 감사. |
| 🐳 | **한 줄로 셀프 호스팅** | `docker compose up`으로 전체 스택 기동 (manager + MySQL + Qdrant + frontier). SaaS 의존성 없음. |
| 📊 | **가관측성 전체 스택 내장** | Prometheus (메트릭) / Loki (로그) / Tempo (트레이스) / Grafana (대시보드)가 자동 배포. 자연어로 질문하면 Agent가 PromQL / LogQL / TraceQL을 작성. |
| 🧠 | **원하는 모델 사용** | Anthropic / OpenAI / GLM / DeepSeek / Gemini / Kimi, 그 외 OpenAI 호환 엔드포인트. 프로바이더 라우팅과 기본 모델 전환은 재시작 없이 즉시 반영. |
| 💬 | **양방향 IM 채널** | Slack / Telegram / Larksuite (Feishu) / DingTalk / WeCom. 팀이 평소 대화하는 곳에서 그대로 질문. 채널별 allow-list와 채널별 로케일. |
| 🛠️ | **읽기 전용 호스트 도구, 모든 호출 감사** | bash (샌드박스), `host_probe_*`, `query_promql`, `expand_topology` 등 26+ 도구. Viewer 역할은 ClassSafe만. |

## 연동

팀의 가관측성, 채널, 모델 스택에 그대로 연동됩니다.

| | |
|---|---|
| **가관측성** | <img src="https://api.iconify.design/logos:prometheus.svg" alt="Prometheus" title="Prometheus" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:grafana.svg" alt="Grafana" title="Grafana" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/loki.svg" alt="Loki" title="Loki" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/tempo.svg" alt="Tempo" title="Tempo" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/opentelemetry.svg" alt="OpenTelemetry" title="OpenTelemetry" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:qdrant-icon.svg" alt="Qdrant" title="Qdrant" width="28" height="28" /> |
| **채널** | <img src="https://api.iconify.design/logos:slack-icon.svg" alt="Slack" title="Slack" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:telegram.svg" alt="Telegram" title="Telegram" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/larksuite.svg" alt="Larksuite" title="Larksuite" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/dingtalk.svg" alt="DingTalk" title="DingTalk" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.simpleicons.org/wechat" alt="WeCom" title="WeCom" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://api.iconify.design/logos:webhooks.svg" alt="Webhook" title="Webhook" width="28" height="28" /> |
| **모델** | <img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/claude-color.svg" alt="Anthropic" title="Anthropic" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/openai.svg" alt="OpenAI" title="OpenAI" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/gemini-color.svg" alt="Gemini" title="Gemini" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/deepseek-color.svg" alt="DeepSeek" title="DeepSeek" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="docs/assets/integrations/zhipu.svg" alt="Zhipu" title="Zhipu" width="28" height="28" />&nbsp;&nbsp;&nbsp;<img src="https://cdn.jsdelivr.net/npm/@lobehub/icons-static-svg@latest/icons/kimi-color.svg" alt="Kimi" title="Kimi" width="28" height="28" /> |

## 라이선스

Apache 2.0 — [LICENSE](LICENSE) 참조.
