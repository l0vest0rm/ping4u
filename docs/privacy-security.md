# Privacy & security / 隐私与安全

Updated / 更新日期：2026-11-14

[English README](../README.md) · [中文首页](../README.zh-CN.md)

## 中文

本文介绍 Ping4U 的连接保护、凭据存储和数据处理范围，帮助你了解使用产品时哪些数据会被哪些服务处理。这是技术说明，不替代完整隐私政策，也不构成第三方安全认证。

### 工作在哪里运行

Agent 和终端进程运行在你的 Host 电脑上。手机发送操作，并接收会话内容或终端状态。手机发起的任务仍使用 Host 的项目文件和执行环境。

Agent 调用远端模型或联网工具时，可能发送提示词、相关代码、上下文和工具输出。请根据项目的数据要求选择 Agent、模型供应商和工具权限。

### 手机与 Host 的连接

Ping4U 的远程业务消息通过 WebRTC DataChannel 传输，并使用 DTLS 保护。信令采用 Ed25519 签名，绑定两端身份、会话、角色、消息顺序和内容。传输层要求远端 SDP 中包含一致的 SHA-256 DTLS 指纹，由 WebRTC 栈进行证书匹配。

在端点身份可信、签名和指纹验证正确执行的前提下，业务数据在 Host 与客户端之间加密传输。需要 TURN 中继时，中继转发加密传输数据，不作为业务明文的解密端点。

这一保护范围是 **Host 与客户端之间的业务数据链路**。信令签名用于验证真实性和完整性，不会隐藏信令内容。账号信息、连接元数据、使用统计和模型请求具有各自的数据处理范围；连接服务仍可能观察网络地址、连接时间、路由信息和流量规模。

### 配对与访问权限

在电脑上生成配对码，在手机上输入，再由 Host 用户确认设备和访问权限。请只接受认识的设备，不要分享配对码。

查看输出和输入终端命令是不同权限。需要手机输入时，在桌面端开启对应权限，并检查当前访问状态。重新连接后，先确认任务状态，避免重复提交结果未知的操作。

撤销访问权限不能撤回已经执行的命令、已经修改的文件或已经送达另一端的内容。

### 模型服务与 Routing

模型供应商会处理 Agent 发出的请求。使用 Routing 时，请确认所选账号、服务地址和模型。手机与 Host 之间的传输保护，不改变模型供应商处理提示词及相关上下文的事实。

模型服务的数据保留、训练使用和删除规则以对应供应商政策为准。Ping4U 不对不同供应商作统一的零保留或不训练承诺。

### 本地凭据保护

macOS Host 身份存储采用应用管理的 AES-256-GCM 加密文件，包裹密钥保存在同一用户的受限权限文件中。这有助于减少意外明文泄露，但不能抵御该用户权限或整个数据目录已被攻陷的情况。

不同平台和 Agent 使用各自的凭据存储机制。Agent 自身的账号与历史受其原有存储机制约束；不要假设所有凭据都使用系统钥匙串或硬件保护。

### 使用统计

客户端包含两个低频产品事件：

| 事件 | 触发方式 |
|---|---|
| `app.started` | 应用进程启动时记录 |
| `app.used` | 首次真实前台操作触发，按 UTC 日期每安装每天去重 |

这些事件包含随机安装标识、进程会话标识、时间、平台和应用版本。产品事件接口不包含提示词、代码、终端输入、文件路径或配对码。

桌面事件在有效登录状态下可以关联账号。手机事件不归给所配对 Host 的账号，但随机安装标识仍可关联同一次安装的事件。

当前没有 App 内的图形化统计开关。桌面端可在应用启动前设置环境变量 `PING4U_ANALYTICS_DISABLED=1`，禁用这套统计的采集与发送。手机端使用平台偏好设置控制统计，尚无 App 内操作入口。

关闭产品统计不等于关闭账号、安全或连接服务所需的数据处理。上述字段范围仅适用于产品事件接口，不涵盖所有服务日志；本文不对这些服务的数据保留期限作统一承诺。

### 设备与内容安全

连接加密不能防止已被攻陷的电脑或手机读取其可见内容，也不能撤销已授权 Agent 的操作。请保护设备登录、核对工具权限，并在分享日志或截图前移除凭据、配对码、私有代码和个人信息。不要在公开 Issue 中发布安全漏洞利用细节或敏感数据。

## English

This page explains Ping4U's connection protection, credential storage and data processing scope. It is a technical overview, not a substitute for a complete privacy policy or a third-party security certification.

### Where work runs

Agents and terminals run on your Host computer. A phone sends actions and receives conversation content or terminal state. Tasks started from a phone still use the Host's project files and execution environment.

Agents calling remote models or online tools may send prompts, relevant code, context and tool output. Choose agents, model providers and tool permissions according to your project's data requirements.

### Phone-to-Host connections

Ping4U carries remote application messages over WebRTC DataChannel with DTLS protection. Ed25519-signed signaling binds endpoint identities, session, role, message sequence and content. The transport requires a consistent SHA-256 DTLS fingerprint in remote SDP, with certificate matching performed by the WebRTC stack.

With trusted endpoint identities and correctly enforced signature and fingerprint validation, application data is encrypted between Host and client. A TURN relay forwards encrypted transport data rather than acting as an application-plaintext endpoint.

This protection covers the **application data connection between Host and client**. Signatures authenticate signaling and protect its integrity; they do not conceal its content. Account information, connection metadata, analytics and model requests have separate processing boundaries. Connection services may observe network addresses, timing, routing information and traffic volume.

### Pairing and access

Generate a pairing code on the computer, enter it on the phone, and confirm the device and its access permissions on the Host. Only approve devices you recognize, and do not share pairing codes.

Viewing output and entering terminal commands are distinct permissions. Enable the relevant permission on desktop when you need phone input, and check the current access state. After reconnecting, inspect task status before resubmitting an operation whose outcome is unknown.

Revocation cannot undo commands already executed, file changes already made or content already delivered.

### Model services and Routing

Model providers process requests sent by agents. When using Routing, check the selected account, service address and model. Phone-to-Host encryption does not prevent the model provider from processing prompts and related context.

Retention, training use and deletion rules depend on the provider's policy. Ping4U makes no blanket zero-retention or no-training promise across providers.

### Local credentials

The macOS Host identity store uses application-managed AES-256-GCM encrypted files. Its wrapping key is held in a restricted file owned by the same user. This helps reduce accidental plaintext disclosure, but does not protect against compromise of that user or the data directory.

Platforms and agents have their own credential-storage mechanisms. Agent accounts and history remain subject to the agent's storage mechanisms; do not assume every credential uses an OS vault or hardware protection.

### Usage analytics

The client includes two low-volume events:

| Event | Trigger |
|---|---|
| `app.started` | Application process launch |
| `app.used` | First real foreground interaction, deduplicated per installation per UTC day |

Fields include a random installation identifier, process-session identifier, time, platform and app version. The product-event interface does not include prompts, code, terminal input, file paths or pairing codes.

Desktop events may be associated with a signed-in account. Mobile events are not attributed to the paired Host's account, although the installation identifier allows correlation within that installation.

There is currently no in-app graphical analytics toggle. Starting the desktop app with the environment variable `PING4U_ANALYTICS_DISABLED=1` disables this event collection and sending. Mobile apps use platform preference settings, with no in-app control currently available.

Disabling product analytics does not disable processing required by account, security or connection services. The field list above applies to the product-event interface, not every service log. This page makes no uniform retention-period commitment for those services.

### Device and content security

Transport encryption does not protect visible content from compromised endpoints or undo actions by authorized agents. Protect device access, check tool permissions, and remove credentials, pairing codes, private code and personal information before sharing logs or screenshots. Do not post exploit details or sensitive data in public issues.
