# Privacy & security / 隐私与安全说明

Technical overview · 2026-11-14 · 技术说明审阅稿

This document explains the implementation reviewed for these materials. It is not an independent security audit, a certification, or a complete legal privacy policy. Release-specific behavior and operational retention policies require separate confirmation.

本文说明此次资料准备所核对到的实现，不代表独立安全审计、认证或完整法律隐私政策。具体发行版行为和线上数据保留政策仍需分别确认。

## 中文

### 1. 工作在哪里运行

Ping4U 的 Agent 和终端进程在 Host 电脑上运行。手机连接 Host，发送操作并接收会话内容或终端状态。项目执行环境在 Host，不会因为手机发起任务就变成手机本地执行。

“在自己的电脑执行”不等于“所有数据都不出电脑”。Agent 调用远端模型、启用联网工具或使用外部服务时，相应内容可能离开 Host。

### 2. 手机与 Host 的连接保护

已核对的传输实现使用 WebRTC DataChannel 承载业务消息，通过 DTLS 保护传输；信令使用 Ed25519 签名，绑定两端身份、会话、角色、消息顺序和消息内容。传输层要求远端 SDP 中存在一致的 SHA-256 DTLS 指纹，由 WebRTC 栈进行证书匹配。

在两端身份可信、签名与指纹验证正确执行的前提下，Host 与客户端之间的业务数据由两端加密传输。需要 TURN 中继时，中继转发的是加密传输数据，不应成为业务明文的解密端点。

这一说明的范围是 **Host 与客户端之间的业务数据链路**。它不表示信令内容被加密到服务端不可见，也不表示账号、连接元数据、日志、使用统计或模型请求都处于同一端到端加密边界。签名提供真实性和完整性校验，不等于隐藏信令内容。

### 3. 配对与权限

产品通过配对码发现并连接设备，由 Host 用户确认设备与访问权限。配对不是无限授权；查看输出、终端输入和其他操作应分别服从 Host 的授权状态。

不要分享配对码，只接受认识的设备。撤销设备权限不能撤回已经执行的命令、已经修改的文件，或已经到达另一端的内容。撤权、重连与过期在各发行版及真实网络中的行为，需要专门验证。

### 4. 模型服务与 Routing

Agent 可能向所选择的模型供应商发送提示词、相关代码、上下文和工具输出。使用 Routing 时，请同时确认所选账号、服务地址和模型；Routing 管理兼容工具的接入，不会消除供应商处理请求的事实。

手机到 Host 的传输保护不延伸为“模型供应商看不到提示词”。供应商如何保存或使用数据，应查看对应服务的政策。本文不作统一的零保留或不训练承诺。

### 5. 本地凭据保护

已核对的 macOS Host 身份存储使用应用管理的 AES-256-GCM 加密文件，其包裹密钥保存在同一用户的受限权限文件中。该设计有助于避免意外明文泄露，但不能抵御同一用户权限或整个数据目录已被攻陷的情况。

这不是“所有密钥均进入系统钥匙串”或“硬件级不可导出”的保证。不同平台及不同 Agent 的凭据存储分别实现；Agent 自身的账号和历史仍受其原有存储机制约束。

### 6. 账号、连接信息和使用统计

账号登录、连接建立及运行服务会处理相应身份和连接信息。会合、信令与中继服务可能观察连接时间、网络地址、路由信息和流量规模；加密业务内容不会自动隐藏这些元数据。

已核对的客户端实现包含两个低频产品事件：

| 事件 | 用途与频率 |
|---|---|
| `app.started` | 应用进程启动时记录 |
| `app.used` | 首次真实前台操作触发，按 UTC 日期每安装每天去重 |

事件包含随机安装标识、进程会话标识、时间、平台和应用版本等字段。这套统计接口不包含提示词、代码、终端输入、文件路径或配对码。桌面事件在具备有效登录状态时可以关联账号；手机事件按当前实现匿名上报，不归给所配对 Host 的账号。这里的“匿名”不是不可关联保证，随机安装标识仍可关联同一次安装的事件。

当前实现没有面向普通用户的图形化统计开关；桌面在启动前设置 `PING4U_ANALYTICS_DISABLED=1` 可禁用这套统计采集与发送。手机实现有平台偏好设置，但本文不将其描述为现成的 App 内开关。禁用产品统计不等于关闭账号、安全或网络服务所需的全部处理。

上述范围仅限这套产品事件，不能据此宣称整个产品“零数据收集”或所有组件“零日志”。正式隐私政策还需明确运营主体、联系渠道、各类数据的保留和删除规则。

### 7. 保护边界

连接加密不能防止已被攻陷的 Host 或手机读取其可见内容，也不能阻止已授权的 Agent 执行不当操作。模型输出、工具权限与本地文件访问仍需用户判断和控制。

本说明依据实现与文档核对，未在本次工作中执行独立渗透测试、真实跨网攻击验证或各平台完整安全验收。请勿将其包装成“已审计 E2E 安全认证”。安全漏洞应使用负责人公布的私密报告渠道，不要在公开 Issue 中上传凭据或漏洞利用细节。

## English

### Execution and transport

Agents and terminals run on the Host computer. A phone sends actions and receives conversation content or terminal state. Local execution does not mean that no data leaves the computer: agents may call remote models and external tools.

The reviewed implementation carries application messages over WebRTC DataChannel with DTLS transport protection. Ed25519-signed signaling binds the endpoints, session, role, message sequence and content. The transport requires a consistent SHA-256 DTLS fingerprint in remote SDP, with certificate matching performed by the WebRTC stack.

With trusted endpoint identities and correctly enforced signature and fingerprint validation, application data is encrypted between Host and client. A TURN relay forwards encrypted transport data rather than acting as an application-plaintext endpoint. This scope does not cover every service interaction: signed signaling is not necessarily confidential from the signaling service, and account records, connection metadata, analytics and model calls have separate boundaries.

### Pairing and permissions

Pairing connects a device subject to the Host user's confirmation and access settings. Viewing output and entering commands are distinct permissions. Only approve devices you recognize. Revocation cannot undo commands already executed, file changes already made, or content already delivered. Release-specific reconnection, expiry and revocation behavior needs dedicated validation.

### Models and local credentials

Configured model services may receive prompts, relevant code, context and tool output. Routing manages supported connections; it does not prevent the selected provider from processing requests. Consult that provider's policies. This document makes no blanket zero-retention or no-training promise.

The reviewed macOS Host identity store uses application-managed AES-256-GCM encrypted files with a wrapping key held in a restricted file owned by the same user. It helps prevent accidental plaintext disclosure, but does not protect against compromise of that user or the data directory. This is not a claim that every key uses an OS credential vault or hardware-backed non-exportable storage. Other platforms and agent credentials have their own storage implementations.

### Account information and analytics

Account and connection services process the identity and connection information needed for their operations. Rendezvous, signaling and relay services may observe network addresses, timing, routing information and traffic volume. Content encryption does not conceal all metadata.

The reviewed client includes two low-volume events: `app.started` per process launch and `app.used`, triggered by real foreground interaction and deduplicated per installation per UTC day. Fields include a random installation identifier, process-session identifier, time, platform and app version. This event interface does not include prompts, code, terminal input, file paths or pairing codes.

Desktop events may be associated with a signed-in account. Mobile events are currently anonymous rather than attributed to the paired Host's account; an installation identifier still allows correlation within that installation. The current implementation has no ordinary in-app graphical analytics toggle. Starting the desktop app with `PING4U_ANALYTICS_DISABLED=1` disables this event collection and sending. Mobile implementations have platform preference settings, not a documented user-facing toggle here.

These statements concern the product-event interface, not every log or service in the system. A complete privacy policy must separately define the operator, contact information, retention and deletion rules.

### Limits

Transport encryption does not protect content from compromised endpoints or undo actions by authorized agents. This review did not perform an independent security audit, penetration test, or complete cross-platform and cross-network security acceptance. Do not describe this document as an audited E2E certification. Use a privately published security-reporting channel for vulnerabilities, not a public issue containing exploit details or credentials.
