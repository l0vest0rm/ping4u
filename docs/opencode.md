# OpenCode in Ping4U / 在 Ping4U 中使用 OpenCode

[Getting started / 快速开始](getting-started.md)

## 中文

OpenCode 是 Ping4U 接入的编程 Agent 之一。Ping4U 提供按项目组织的会话界面和手机访问入口；OpenCode 在 Host 电脑上运行。

### 版本范围

当前核对到的集成资料记录了 OpenCode **2.1.4** 的原生 HTTP profile 验证范围。这不是对全部 OpenCode V2 版本的兼容承诺，也没有据此确认 V1 可用。以所安装 Ping4U 的兼容性提示为准，不要为了试用擅自降级已有 OpenCode 环境。

### 使用步骤

1. 在 Host 上正常安装并登录受支持的 OpenCode，保留已有配置和认证。
2. 在 Ping4U 的「Agent 管理」中确认 OpenCode 能被识别，检查版本和状态。
3. 打开项目，选择 OpenCode，新建会话并发送一条简短任务。
4. 确认输出来自目标项目，记录 Ping4U 和 OpenCode 版本。
5. 需要手机访问时，按[快速开始](getting-started.md)配对，再打开刚才的会话继续。

如需由 Routing 管理模型，单独完成账号、模型和 OpenCode 工具接入配置，再验证真实请求。手机连接、Agent 集成和模型接入分别检查，不把其中一项成功视为全部成功。

若出现不支持的版本、认证错误或历史读取失败，先保留版本号和不含敏感内容的错误信息。不要将历史读取失败直接判断为数据库损坏，也不要为排查删除原会话或凭据。

## English

OpenCode is one of Ping4U's coding-agent integrations. Ping4U provides project-based sessions and phone access; OpenCode runs on the Host computer.

The integration material reviewed for this draft records the native HTTP profile's verification scope as **OpenCode 2.1.4**. This does not establish compatibility with every V2 release or with V1. Follow the compatibility checks in your installed Ping4U release; do not downgrade an existing environment just to try this guide.

1. Install and authenticate a supported OpenCode version on the Host using its normal installation channel.
2. Check its detected version and state in Ping4U's Agent Management.
3. Open a project, select OpenCode, create a session and send a small task.
4. Confirm that the response belongs to the intended project and record both application versions.
5. Optionally pair a phone and continue that same session.

If using Routing, configure the account, model and OpenCode connection separately, then verify an actual request. Agent integration, model access and phone connectivity are separate checks. If history cannot be read, preserve the error and versions; do not assume database corruption or delete existing sessions and credentials.
