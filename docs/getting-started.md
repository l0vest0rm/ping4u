# Getting started / 快速开始

[English README](../README.md) · [中文首页](../README.zh-CN.md)

## 中文

### 1. 安装并打开桌面端

访问[官方下载页](https://ping4u.cc/downloads)，选择电脑对应的平台，按照页面说明完成安装。打开 Ping4U，按提示使用邮箱验证码登录。

桌面端所在的电脑是 Host，负责运行 Agent、项目文件操作和终端。先完成桌面端的第一项任务，再按需要连接手机。

### 2. 检查 Agent

在「Agent 管理」中查看工具的安装、登录与版本状态。按该工具和安装渠道的提示完成准备。已有的 Agent 账号和配置仍需要符合该工具要求；Ping4U 登录不等于所有 Agent 都已登录，也不等于已获得模型额度。

首次体验可选择自己已经安装、登录且受当前 Ping4U 支持的工具。打开项目目录，新建会话，发送一条容易判断结果的任务，例如：「解释这个项目的目录结构，先不要修改文件。」

确认返回内容对应当前项目。要继续原对话，请选择原会话；创建另一种 Agent 的会话不会自动复制上下文。

### 3. 使用终端

切换到「终端」，选择或创建终端会话。先核对当前项目和目录，再执行命令。终端运行在 Host 上，使用 Host 的操作系统、文件和环境，不在手机里运行。

### 4. 按需配置 Routing

已有 Agent 配置能满足需要时，可以暂不使用 Routing。

需要管理账号与模型时，打开 Routing，在「账号与密钥」中添加受支持的服务，按提示登录或填写 API Key，读取可用模型。在「工具接入」中选择兼容的工具、账号和模型，检查配置后应用。

应用配置后，用一个新会话确认请求真正成功。配置保存成功不等于模型请求成功，也不保证所有订阅、模型、协议和工具可任意组合。模型费用及额度以对应服务为准。

### 5. 连接手机

1. 从官方下载页安装对应的手机 App。
2. 在电脑上进入「手机连接」，生成配对码。
3. 在手机上选择连接电脑，输入配对码。
4. 回到电脑核对设备名称，确认连接和访问权限。
5. 在手机进入项目，选择原会话继续，或新建 Host 上的会话。

需要从手机输入终端命令时，在桌面的手机访问设置中开启终端输入，并确认当前输入权限。只读访问和可以输入不是同一权限。

配对码过期时重新生成。连接失败时，先检查 Host 服务、两端网络、设备授权和版本。电脑休眠、关机或服务停止时，手机无法继续访问。重新连接后先确认任务状态，避免把结果未知的操作重复提交。

## English

### Install the desktop app

Visit [Downloads](https://ping4u.cc/downloads), choose your platform, and follow its installation instructions. Open Ping4U and complete email verification.

This computer is the Host. It runs the agents, file operations and terminals. Complete a first desktop task before adding a phone.

### Check your agent and open a project

Use Agent Management to check installation, authentication and version compatibility. Follow the instructions for that tool and its installation channel. Signing in to Ping4U does not sign in to every agent or provide model credits.

Choose an installed, authenticated and supported agent. Select a project, create a session, and try a small task: “Explain this project's directory structure without changing files.” Check that the answer refers to the selected project. Continue the original session to retain its conversation; a different agent session does not automatically inherit that context.

### Use a terminal

Switch to Terminal and create or select a session. Check its working directory before running a command. The terminal uses the Host's operating system, files and environment.

### Configure Routing if needed

Routing is optional when your existing agent configuration meets your needs. To configure it, open Accounts & Keys, add a supported service, authenticate or supply an API key, and load its models. In Tool Connections, select a compatible tool, account and model, review the configuration, and apply it.

Verify the result with a real request in a new session. Saving a configuration does not prove a successful model call. Subscription, model, protocol and tool compatibility varies; provider charges and limits still apply.

### Pair a phone

Install the mobile app from the download page. On the computer, open Phone Connection and generate a pairing code. Enter it on the phone, then check the device name and approve access on the computer. Open the project on the phone to continue a session or start a new one on the Host.

Enable terminal input in desktop phone-access settings when you need it, and check the current input permission. For connection problems, check the Host service, both networks, device authorization, app versions and pairing-code expiry. The Host must remain available. After reconnecting, inspect task status before resubmitting an operation whose outcome is unknown.
