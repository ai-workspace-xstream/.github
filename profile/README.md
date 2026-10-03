<p align="center">
  <img src="https://raw.githubusercontent.com/ai-workspace-xstream/.github/main/assets/xconnect-homepage-hero.png" alt="XConnect secure connectivity for AI workspaces" width="100%" />
</p>

<h1 align="center">ai-workspace-xstream</h1>
<p align="center"><strong>AI 工作区安全连接与边缘运行时</strong></p>

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

## 组织概览

XConnect 为 AI 工作区提供安全连接、边缘节点管理和跨平台客户端。Proxy-Server 路线面向代理节点部署；XConnect Zero 路线通过 Gateway 与 One 连接受控设备。

[完整中文介绍](https://github.com/ai-workspace-xstream/.github/blob/main/profile/README-zh.md) · [English overview](https://github.com/ai-workspace-xstream/.github/blob/main/profile/README-en.md)

## 🏛️ 四大核心支柱

<table>
<tr>
<td width="25%" align="center" valign="top">
<h3>零信任控制面</h3>
<p align="left"><sub>设备身份、一次性邀请、签名配置与会话续期，连接受控节点。</sub></p>
</td>
<td width="25%" align="center" valign="top">
<h3>边缘节点与中继</h3>
<p align="left"><sub>Edge Agent 同步节点配置；Gateway 提供 Linux 服务端中继。</sub></p>
</td>
<td width="25%" align="center" valign="top">
<h3>受控客户端</h3>
<p align="left"><sub>One 支持 macOS、Linux、Windows；App 提供桌面与移动端界面。</sub></p>
</td>
<td width="25%" align="center" valign="top">
<h3>可观测与运维</h3>
<p align="left"><sub>Xray 指标、节点日志、诊断与运行手册支撑连接验收。</sub></p>
</td>
</tr>
</table>

---

## 📦 核心仓库矩阵

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

## 🚀 部署路线

完整说明见：[XConnect / Proxy-Server 部署路线总览](https://github.com/ai-workspace-xstream/docs/blob/main/runbooks/2026-10-03-xconnect-deployment-routes.md)。

| 路线 | 控制面 | 组件与平台 |
| --- | --- | --- |
| Proxy-Server 独立部署 | standalone | Linux 节点、Caddy、Xray |
| Proxy-Server Full Stack | Accounts + Vault | Edge Agent、证书同步、自监控 |
| 数据面组件安装 | 安装后继续配置与注册 | Gateway：Linux；One：macOS / Linux / Windows |
| XConnect Zero Full Stack | Zero API | Gateway / One 注册、签名配置、ACK |

按部署指南选择对应路线；CLI 安装、网络注册和业务连通验收分别执行。

---

<p align="center">
  <a href="https://github.com/ai-workspace-xstream/docs/blob/main/runbooks/2026-10-03-xconnect-deployment-routes.md"><strong>完整部署路线文档</strong></a><br />
  <sub>Secure · Signed · Observable · Cross-platform</sub>
</p>
