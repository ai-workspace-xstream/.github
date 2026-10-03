<p align="center">
  <img src="https://raw.githubusercontent.com/ai-workspace-xstream/.github/main/assets/xconnect-homepage-hero.png" alt="XConnect secure connectivity for AI workspaces" width="100%" />
</p>

<h1 align="center">ai-workspace-xstream</h1>
<p align="center"><strong>Secure connectivity and edge runtimes for AI workspaces</strong></p>

<p align="center">
  <a href="https://console.svc.plus/products/xconnect"><img src="https://img.shields.io/badge/XConnect-Console-0B5C7A?style=for-the-badge" alt="XConnect Console" /></a>
  <a href="https://github.com/ai-workspace-xstream"><img src="https://img.shields.io/badge/GitHub-Organization-181717?style=for-the-badge&logo=github" alt="GitHub Organization" /></a>
  <a href="https://github.com/ai-workspace-xstream/xconnect-gateway"><img src="https://img.shields.io/badge/Gateway-Linux-2563EB?style=for-the-badge" alt="Gateway Linux" /></a>
  <a href="https://github.com/ai-workspace-xstream/xconnect-one"><img src="https://img.shields.io/badge/One-Cross--Platform-2F855A?style=for-the-badge" alt="One Cross-platform" /></a>
</p>

<p align="center">
  <a href="https://github.com/ai-workspace-xstream/.github/blob/main/profile/README-zh.md">简体中文</a> ｜ <a href="https://github.com/ai-workspace-xstream/.github/blob/main/profile/README-en.md">English</a>
</p>

---

## 🇬🇧 Organization overview

`ai-workspace-xstream` is the connectivity and edge-runtime organization for AI Workspace. We build the XConnect Zero Trust network as independently releasable, verifiable, and operable components: a control-plane contract, Linux Gateway, edge agent, controlled client CLI, cross-platform app, telemetry exporter, and operational documentation.

The system keeps network roles separate. The control plane owns identity and signed configuration; Gateway owns server-side relay; Edge Agent owns node synchronization; One and XConnect App own the controlled client runtime.

### Mission and delivery principles

* **One control-plane authority:** clients and nodes consume protected APIs and signed configuration instead of accessing the control-plane database directly.
* **Signed configuration and immutable artifacts:** reject unsigned, expired, cross-network, or cross-Gateway configuration; verify release artifacts with explicit versions and `SHA256SUMS`.
* **Runtime-only secrets:** invitations, tokens, private keys, and TLS material are injected at runtime or kept in protected directories, never committed to Git or printed in logs.
* **Separated runtime roles:** Gateway, Edge Agent, One, and the App own separate state and lifecycle boundaries.
* **End-to-end verification:** service state alone is not acceptance; verify the WireGuard handshake, data plane, ACK, and a real target response.

### Main entry points

* [XConnect Console](https://console.svc.plus/products/xconnect)
* [Deployment routes runbook](https://github.com/ai-workspace-xstream/docs/blob/main/runbooks/2026-10-03-xconnect-deployment-routes.md)
* [Architecture and operations docs](https://github.com/ai-workspace-xstream/docs)
* [Client releases](https://github.com/ai-workspace-xstream/xconnect-app/releases)

---

## 🏛️ Core pillars

<table>
<tr>
<td width="25%" align="center" valign="top">
<h3>Zero Trust</h3>
<p align="left"><sub>Device identity, short-lived invitations, signed configuration and session renewal.</sub></p>
</td>
<td width="25%" align="center" valign="top">
<h3>Edge & Relay</h3>
<p align="left"><sub>Edge Agent manages node synchronization; Gateway provides the Linux relay runtime.</sub></p>
</td>
<td width="25%" align="center" valign="top">
<h3>Controlled Clients</h3>
<p align="left"><sub>One CLI supports macOS, Linux and Windows; the App provides desktop and mobile interfaces.</sub></p>
</td>
<td width="25%" align="center" valign="top">
<h3>Observability</h3>
<p align="left"><sub>Xray metrics, node logs, diagnostics and documented operational acceptance.</sub></p>
</td>
</tr>
</table>

---

## 🔄 From signed configuration to a usable connection

```mermaid
flowchart LR
    A[Control Plane<br/>Identity & Signed Config] --> B{Runtime Role}
    B --> C[Gateway<br/>Linux Relay]
    B --> D[Edge Agent<br/>Node Sync & Xray]
    B --> E[One CLI<br/>Controlled Client]
    F[XConnect App<br/>Desktop & Mobile] -. optional integration .-> E
    C --> G[WireGuard / Xray Data Plane]
    D --> G
    E --> G
    G --> H[Handshake · ACK · Target Response]
    style A fill:#DBEAFE,stroke:#3B82F6
    style B fill:#FEF3C7,stroke:#F59E0B
    style C fill:#ECFDF5,stroke:#10B981
    style D fill:#ECFDF5,stroke:#10B981
    style E fill:#F3E8FF,stroke:#8B5CF6
```

1. The control plane issues short-lived credentials and signed configuration bound to a device or Gateway.
2. Gateway, Edge Agent, or One validates the configuration locally and writes only to its protected state directory.
3. Xray and WireGuard establish the data plane; each client uses only its own interface and state.
4. Acceptance verifies service state, the latest handshake, ACK, and a real target response.

---

## 📦 Repository map

| Repository | Type / role | Description |
| --- | --- | --- |
| [`xconnect-gateway`](https://github.com/ai-workspace-xstream/xconnect-gateway) | `Linux Relay Runtime` | Independent Linux Gateway for enrollment, session renewal, signed Gateway configuration, and WireGuard/Xray application. |
| [`xconnect-edge-agent`](https://github.com/ai-workspace-xstream/xconnect-edge-agent) | `Edge Control Agent` | Node-side agent for configuration sync, heartbeats, Xray lifecycle, and the Caddy HTTPS/TLS entry point. |
| [`xconnect-one`](https://github.com/ai-workspace-xstream/xconnect-one) | `Controlled Client CLI` | Independent Go CLI for the device-bound WireGuard/Xray client runtime and local state. |
| [`xconnect-app`](https://github.com/ai-workspace-xstream/xconnect-app) | `Desktop & Mobile Client` | Flutter client for node import, proxy modes, tunnel workflows, diagnostics, and platform packages. |
| [`xray-exporter`](https://github.com/ai-workspace-xstream/xray-exporter) | `Telemetry Exporter` | Exports Xray/V2Ray Stats API and access-log data as Prometheus metrics. |
| [`docs`](https://github.com/ai-workspace-xstream/docs) | `Architecture & Runbooks` | Requirements, plans, architecture, decisions, runbooks, incidents, and release records. |
| [`.github`](https://github.com/ai-workspace-xstream/.github) | `Organization Profile` | Organization-level overview, project entry points, and collaboration boundaries. |

---

## 🚀 Deployment routes

See the complete [XConnect / Proxy-Server deployment routes runbook](https://github.com/ai-workspace-xstream/docs/blob/main/runbooks/2026-10-03-xconnect-deployment-routes.md).

| Route | Control plane | Components / platforms |
| --- | --- | --- |
| Standalone Proxy-Server | Standalone | Linux node with Caddy and Xray |
| Full Stack Proxy-Server | Accounts + Vault | Edge Agent, TLS synchronization and monitoring |
| Data-plane components | Install before enrollment | Gateway: Linux; One: macOS / Linux / Windows |
| Full Stack XConnect Zero | Zero API | Gateway and One enrollment, signed config and ACK |

Choose a route in the deployment guide. CLI installation and network enrollment are separate steps.

---

<p align="center">
  <a href="https://github.com/ai-workspace-xstream/docs/blob/main/runbooks/2026-10-03-xconnect-deployment-routes.md"><strong>Complete deployment guide</strong></a><br />
  <sub>Secure · Signed · Observable · Cross-platform</sub>
</p>
