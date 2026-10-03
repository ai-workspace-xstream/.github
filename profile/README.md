<p align="center">
  <img src="../assets/xconnect-homepage-hero.png" alt="XConnect secure connectivity for AI workspaces" width="100%" />
</p>

<p align="center">
  <a href="https://console.svc.plus/products/xconnect"><strong>🚀 XConnect Console</strong></a>
  ·
  <a href="https://github.com/ai-workspace-xstream/xconnect-app/releases"><strong>📱 Client Releases</strong></a>
  ·
  <a href="https://github.com/ai-workspace-xstream/docs"><strong>📚 Documentation</strong></a>
</p>

<p align="center">
  <a href="https://github.com/ai-workspace-xstream"><img src="https://img.shields.io/badge/GitHub-ai--workspace--xstream-181717?style=flat-square&logo=github" alt="GitHub organization" /></a>
  <a href="https://github.com/ai-workspace-xstream/xconnect-one"><img src="https://img.shields.io/badge/Runtime-XConnect%20One-2563EB?style=flat-square" alt="XConnect One" /></a>
  <a href="https://github.com/ai-workspace-xstream/xconnect-gateway"><img src="https://img.shields.io/badge/Relay-XConnect%20Gateway-7C3AED?style=flat-square" alt="XConnect Gateway" /></a>
  <a href="https://github.com/ai-workspace-xstream/xconnect-app"><img src="https://img.shields.io/badge/Client-Flutter-10B981?style=flat-square&logo=flutter" alt="Flutter client" /></a>
</p>

<p align="center">
  <a href="#中文">🇨🇳 简体中文</a> ｜ <a href="#english">🇬🇧 English</a>
</p>

---

## <a id="中文"></a>🇨🇳 组织概览

`ai-workspace-xstream` 是 AI Workspace 的连接与边缘运行时组织。我们围绕 XConnect Zero Trust 网络，将控制面、Linux Gateway、边缘节点、受控客户端、跨平台 App 与可观测组件拆分为可独立发布、可验证和可运维的开源项目。

我们的目标不是把所有能力塞进一个客户端，而是让每个网络角色拥有清晰的边界：控制面负责身份与签名配置，Gateway 负责服务端转发，Edge Agent 负责节点同步，One 和 XConnect App 负责受控客户端运行时。

### 我们的使命与交付准则

* **控制面唯一可信**：节点和客户端通过受保护的 API 获取设备绑定、签名和过期检查后的配置，不直接访问控制面数据库。
* **签名配置与不可变构件**：拒绝未签名、过期、跨网络或跨 Gateway 的配置；发布制品使用明确版本和 `SHA256SUMS` 校验。
* **运行时最小权限**：邀请、Token、私钥和 TLS 材料只在运行时注入或保存在受保护目录，不进入 Git、日志或公开命令示例。
* **角色与平台隔离**：Linux Gateway、边缘节点、One CLI 和桌面/移动 App 各自维护自己的状态与生命周期，避免共享可变状态。
* **可验证的网络路径**：服务状态、WireGuard handshake、Xray 数据面和目标服务响应分别验证；单个进程 active 不等于端到端连接成功。

### 常用访问入口

* 控制台：[XConnect Console](https://console.svc.plus/products/xconnect)
* 组织主页：[ai-workspace-xstream](https://github.com/ai-workspace-xstream)
* 架构与运行文档：[docs](https://github.com/ai-workspace-xstream/docs)
* 客户端发布：[xconnect-app Releases](https://github.com/ai-workspace-xstream/xconnect-app/releases)

---

## 🏛️ 四大核心支柱

### 🔐 Zero Trust Control Plane

设备身份、一次性邀请、签名配置、会话续期和 ACK 构成网络控制边界。XConnect One 与 Gateway 在本地校验签名、过期时间、网络和角色绑定；控制面实现见 [accounts API](https://github.com/ai-workspace-services/accounts)。

### 🌐 Edge & Relay Runtime

`xconnect-edge-agent` 负责节点侧配置同步、心跳、Xray 生命周期与 Caddy TLS 入口；`xconnect-gateway` 提供独立的 Linux Server relay/service。两者都不把长期凭据或网络邀请写入仓库。

### 💻 Controlled Client Experience

`xconnect-one` 是独立发布的 Go CLI，管理受保护的本地 Xray/WireGuard 运行时；`xconnect-app` 提供 Flutter 桌面与移动端界面、节点管理和诊断能力，并通过明确的插件边界与 CLI 协作。

### 📊 Observable & Operable

`xray-exporter` 将 Xray/V2Ray Stats API 和访问日志转换为 Prometheus 指标；`docs` 集中维护架构、需求、Runbook、故障记录和发布说明。运行验证必须覆盖服务、握手、数据面和用户可见结果。

---

## 🔄 从签名配置到可用连接

```mermaid
flowchart LR
    A[Control Plane<br/>Identity & Signed Config] --> B{Runtime Role}
    B --> C[Gateway<br/>Linux Relay]
    B --> D[Edge Agent<br/>Node Sync & Xray]
    B --> E[One CLI<br/>Controlled Client]
    E --> F[XConnect App<br/>Desktop & Mobile]
    C --> G[WireGuard / Xray Data Plane]
    D --> G
    E --> G
    G --> H[Handshake · ACK · Target Response]
```

1. 控制面签发设备或 Gateway 绑定的短期凭据与签名配置。
2. Gateway、Edge Agent 或 One 在本地验证配置，再写入各自受保护的状态目录。
3. Xray 与 WireGuard 建立数据面连接，客户端只使用自己拥有的接口和状态。
4. 通过服务状态、最新 handshake、ACK 和一个真实目标响应完成验收。

---

## 📦 核心仓库矩阵（7 Repositories）

| 仓库 | 类型 / 定位 | 说明 |
| --- | --- | --- |
| [`xconnect-gateway`](https://github.com/ai-workspace-xstream/xconnect-gateway) | `Linux Relay Runtime` | 独立 Linux Gateway；执行加入、会话续期、签名 Gateway 配置同步、WireGuard/Xray 应用与 ACK。 |
| [`xconnect-edge-agent`](https://github.com/ai-workspace-xstream/xconnect-edge-agent) | `Edge Control Agent` | 节点侧控制代理；同步配置、上报心跳、管理 Xray 生命周期，并由 Caddy 提供 HTTPS/TLS 入口。 |
| [`xconnect-one`](https://github.com/ai-workspace-xstream/xconnect-one) | `Controlled Client CLI` | 独立 Go CLI；管理设备绑定的 WireGuard/Xray 客户端运行时和本地状态。 |
| [`xconnect-app`](https://github.com/ai-workspace-xstream/xconnect-app) | `Desktop & Mobile Client` | Flutter 客户端；提供节点导入、代理模式、Tunnel、诊断和平台打包产物。 |
| [`xray-exporter`](https://github.com/ai-workspace-xstream/xray-exporter) | `Telemetry Exporter` | 采集 Xray/V2Ray Stats API 与访问日志并导出 Prometheus 指标。 |
| [`docs`](https://github.com/ai-workspace-xstream/docs) | `Architecture & Runbooks` | 维护需求、计划、架构、决策、Runbook、故障和发布记录。 |
| [`.github`](https://github.com/ai-workspace-xstream/.github) | `Organization Profile` | 组织级说明、项目入口和协作边界。 |

---

## 🚀 快速入口

### Edge Agent：Linux 节点

在目标节点使用受信任的运行时环境执行；生产环境请先通过 Vault 或其他 Secret Manager 注入凭据，并固定经过审查的 Release/commit。

```bash
curl -fsSL https://raw.githubusercontent.com/ai-workspace-xstream/xconnect-edge-agent/main/scripts/setup-proxy.sh | \
  bash -s -- --node <node-domain>
```

完全独立运行时追加 `--standalone`。该脚本会修改目标主机的依赖、服务、配置和网络设置，不能视为只下载一个 CLI。

### One：受控客户端 CLI

```bash
curl -fsSL https://install.svc.plus/xconnect-one | \
  sudo env XCONNECT_ONE_VERSION=<approved-release-tag> bash
```

安装器只负责下载并校验 CLI；不会自动消费邀请、加入网络、安装外部 Xray/WireGuard 或启动数据面。

### Gateway：Linux Relay

```bash
curl -fsSL https://install.svc.plus/xconnect-gateway | \
  sudo env XCONNECT_GATEWAY_VERSION=<approved-release-tag> bash
```

安装器只负责下载并校验 Gateway CLI；不会执行 enrollment、写入长期凭据、安装 Xray/WireGuard 或启动网络服务。

> 版本标签必须与对应 GitHub Release、`SHA256SUMS` 和托管安装脚本保持一致。安装命令中的 `<approved-release-tag>` 不应替换成未经审查的 `latest`。

---

## 🇬🇧 English

`ai-workspace-xstream` is the connectivity and edge-runtime organization for AI Workspace. We build the XConnect Zero Trust network as independently releasable and verifiable components: a control-plane contract, Linux Gateway, edge agent, controlled client CLI, cross-platform app, telemetry exporter, and operational documentation.

### Mission and delivery principles

* **One control-plane authority:** clients and nodes consume protected APIs and signed configuration instead of accessing the control-plane database directly.
* **Signed configuration and immutable artifacts:** reject unsigned, expired, cross-network, or cross-Gateway configuration; verify release artifacts with explicit versions and `SHA256SUMS`.
* **Runtime-only secrets:** invitations, tokens, private keys, and TLS material are injected at runtime or kept in protected directories, never committed to Git or printed in logs.
* **Separated runtime roles:** Gateway, Edge Agent, One, and the App own separate state and lifecycle boundaries.
* **End-to-end verification:** service state alone is not acceptance; verify the WireGuard handshake, data plane, ACK, and a real target response.

### Core pillars

* **Zero Trust Control Plane** — device identity, short-lived invitations, signed configuration, session renewal, and ACK.
* **Edge & Relay Runtime** — Linux Gateway and Edge Agent for forwarding, synchronization, TLS, and Xray lifecycle management.
* **Controlled Client Experience** — XConnect One CLI and XConnect App for protected local runtimes and diagnostics.
* **Observable & Operable** — Prometheus exporter plus architecture, runbook, incident, and release documentation.

### Repository map

| Repository | Role |
| --- | --- |
| [`xconnect-gateway`](https://github.com/ai-workspace-xstream/xconnect-gateway) | Linux relay runtime |
| [`xconnect-edge-agent`](https://github.com/ai-workspace-xstream/xconnect-edge-agent) | Node-side control agent |
| [`xconnect-one`](https://github.com/ai-workspace-xstream/xconnect-one) | Controlled client CLI |
| [`xconnect-app`](https://github.com/ai-workspace-xstream/xconnect-app) | Desktop and mobile client |
| [`xray-exporter`](https://github.com/ai-workspace-xstream/xray-exporter) | Xray/V2Ray Prometheus exporter |
| [`docs`](https://github.com/ai-workspace-xstream/docs) | Architecture and operations documentation |
| [`.github`](https://github.com/ai-workspace-xstream/.github) | Organization profile and collaboration boundary |

---

📘 **完整部署路线 / Deployment routes:** [XConnect / Proxy-Server 部署路线总览](https://github.com/ai-workspace-xstream/docs/blob/main/runbooks/2026-10-03-xconnect-deployment-routes.md)

Secure · Signed · Observable · Cross-platform · AI-workspace ready
