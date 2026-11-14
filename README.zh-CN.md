<p align="center"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/ping4u-logo-dark.svg"><img src="assets/ping4u-logo.svg" alt="Ping4U" width="160"></picture></p>

# Ping4U

**你的 Agent，你的模型，一个工作空间。**

Ping4U 把编程 Agent 会话和真实终端按项目组织在一起。你可以在电脑上工作，也可以连接手机，在同一台 Host 电脑上发起或继续任务。需要管理模型接入时，再通过可选的 Routing 配置受支持的账号、模型和工具。

[官网](https://ping4u.cc/) · [下载](https://ping4u.cc/downloads) · [快速开始](docs/getting-started.md) · [隐私与安全](docs/privacy-security.md) · [English](README.md)

![Ping4U 桌面、Routing 与手机工作流程](assets/ping4u-preview.gif)

*从现有产品演示中节选的 15 秒预览。[观看 60 秒完整视频](assets/ping4u-demo.mp4)。演示说明工作方式，实际界面和平台能力以所安装版本为准。*

## 用 Ping4U 做什么

- **按项目管理工作。** 在一个工作空间里找到 Agent 会话和终端。
- **选择合适的 Agent。** 接入 Claude Code、Codex、OpenCode 等工具，具体能力取决于受支持的工具版本。
- **使用真实终端。** 命令在 Host 电脑上的项目目录和环境中执行。
- **需要时连接手机。** 从手机新建或继续 Host 上的会话，也可使用已授权的终端。桌面端可以独立使用。
- **通过 Routing 配置模型接入。** 为兼容的工具管理受支持的账号和模型；是否使用、支持哪些组合，由你的需求和当前版本决定。

## 一个工作场景

打开项目，让一个 Agent 审阅修改，再在另一段会话里推进实现；需要运行命令时打开终端。离开电脑后，可以在手机上继续 Ping4U 管理的会话。

不同 Agent 的会话各有上下文，切换 Agent 不会自动转移对话或共享全部历史。

## 开始使用

1. 在[官网下载 Ping4U](https://ping4u.cc/downloads)，按照对应平台说明安装桌面端。
2. 打开 Ping4U，完成登录，在「Agent 管理」中检查本机工具。
3. 选择项目与受支持的 Agent，发起任务；有需要时配置 Routing。
4. 需要手机访问时，从下载页安装对应移动端，通过「手机连接」完成配对。

详细步骤见[快速开始](docs/getting-started.md)和 [OpenCode 说明](docs/opencode.md)。

## 工作在哪里运行

Agent 和终端进程运行在 Host 电脑上，手机访问的是这台电脑的工作空间。远程使用需要 Host 服务和网络保持可用；电脑关机或休眠后，不能把它当作持续运行的云端执行器。

Agent 可能把提示词、相关代码和工具输出发送给所配置的模型服务。手机与 Host 之间的加密连接，不意味着模型服务无法看到这些独立请求。详见[隐私与安全说明](docs/privacy-security.md)。

## 关于本仓库

Ping4U 是闭源产品。本仓库提供产品文档和演示素材，不包含应用源码；公开文档不代表应用开源。

反馈问题时，请提供 Ping4U 版本、电脑和手机系统、Agent 版本、复现步骤与实际结果。分享日志或截图前，请移除密钥、配对码、私有代码和个人信息。安全漏洞详情不要发布到公开 Issue。
