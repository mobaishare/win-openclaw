一个为 Windows 打包的 OpenClaw 桌面应用，目标是：**开箱即用、无需手动安装 Node / openclaw、数据完全在本地目录中可备份/迁移**。

---

## 功能概览

- **内置 OpenClaw Gateway 与 Node 运行时**（独立于系统环境）。
- 双击 `OpenClaw.exe` 即可启动，自动打开 OpenClaw 控制台 UI。
- 内置中文 UI 文案与帮助文档：
- 一键升级内置 OpenClaw 与 Node 的脚本：`升级内置OpenClaw环境.cmd`。

### 1. 获取与运行

- 将打包产物中的 `OpenClaw 0.1.0.exe` 拷贝到任意目录（建议：`D:\Apps\OpenClaw\`）。
- 双击 `OpenClaw 0.1.0.exe` 即可启动。

首次启动会在同级目录下自动创建：

- `openclaw-data\openclaw.json`：OpenClaw 主配置文件。
- `openclaw-data\workspace\`：默认工作区目录（会存放技能、数据等）。
- `openclaw-data\app-log.txt`：桌面应用运行日志。

之后再次双击同一个 exe，即可复用同一份 `openclaw-data`，真正实现「便携 + 不动 C 盘」。

### 2. 首次配置（在应用内完成）

应用内嵌的是 OpenClaw 官方的 **Control UI**，所有设置在这里完成。

1. 等待窗口中「正在启动 OpenClaw...」提示结束，自动进入 Control UI。
2. 在顶部或侧边栏找到：
   - **Config / 配置**：全局配置页面。
   - **Models / 模型**：模型与 API Key 设置。
   - **Skills / 技能**：技能与插件管理。
   - **Channels / 通道**：机器人连接渠道（WebChat 等）。
3. 推荐最小配置流程：
   - 在 **Models** 中配置你将要使用的 LLM（如 DeepSeek、OpenAI、Moonshot 等）。
   - 在 **Skills** 中确认需要的技能已启用（包括你自己写的技能）。
   - 在 **Channels** 中打开 WebChat，方便浏览器中直接聊天测试。

所有修改直接写入 `openclaw-data\openclaw.json` 与相关目录，无需手工编辑文件。

### 3. 中文菜单与数据位置

桌面应用的主菜单为中文，主要入口包括：

- **文件 → 模型配置...**：快速设置默认模型、API Key（DeepSeek / OpenAI / Anthropic / 自定义）与模型 ID，无需改 JSON。
- **文件 → 打开配置文件**：直接在资源管理器中打开 `openclaw-data\openclaw.json` 所在目录。
- **文件 → 打开技能目录**：打开默认工作区的 skills 目录（你可以把自己的技能放在这里）。
- **文件 → 打开数据目录**：打开 `openclaw-data` 根目录，查看日志、工作区等。
- **查看 → 刷新控制台**：刷新当前 Control UI。
- **查看 → 切换开发者工具**：开发调试时查看控制台日志用。

只要你移动 `OpenClaw 0.1.0.exe` 到别的位置重新启动，就会在新的目录生成一份新的 `openclaw-data`，互不影响。

### 4. 常见问题

- **双击 exe 没有任何反应？**
  - 检查目录下是否多开了其它 `OpenClaw.exe` 实例（只允许单例运行）。
  - 查看 `openclaw-data\app-log.txt` 中是否有报错信息。

- **一直停在「正在启动 OpenClaw」？**
  - 可能是内置 Gateway 启动失败，优先查看 `openclaw-data\app-log.txt`。
  - 检查当前目录是否有写入权限（必须能创建 `openclaw-data`）。

- **想要重置配置 / 重新初始化？**
  - 关闭应用后，删除当前目录下的 `openclaw-data`，再重新双击 exe 即可重新走首次启动流程。

### 5. 预装工具与扩展

桌面应用内嵌的 OpenClaw 已包含多种扩展，可在 **完整控制台** 中按需启用：

- **飞书 (Feishu/Lark)**：在 **Channels / 通道** 中启用 Feishu，按提示配置应用凭证即可对接飞书机器人。
- **Web 工具**：`web_fetch`、`web_search` 等可在 **Skills / 工具** 中启用；浏览器自动化可参考 OpenClaw 官方 [Browser 工具](https://docs.openclaw.ai/tools/browser) 文档。
- **GitHub 等**：可在控制台 **Skills / 插件** 中通过「安装插件」添加（如 `openclaw plugins install` 支持的包）。

==============================================

OpenClaw Windows 桌面应用 — 使用说明（桌面版）
==============================================

一、快速开始
------------
1. 解压或复制本文件夹（内含 OpenClaw.exe）。
2. 双击 `OpenClaw.exe` 启动：
   - 首次启动会显示“正在启动 OpenClaw…”页面，并自动启动内置 Gateway。
   - 启动成功后会自动跳转到 OpenClaw 控制台页面。
3. 关闭主窗口后，应用会缩小到系统托盘：
   - 双击托盘图标可以重新打开窗口。

二、数据与配置位置
------------------
本桌面应用的所有数据都放在当前目录下的 `openclaw-data` 中，便于备份和迁移：

- 配置文件：`openclaw-data\openclaw.json`
- 工作区目录：`openclaw-data\workspace\`
- 日志文件：`openclaw-data\app-log.txt`

通过菜单“文件”可以快速打开：

- “打开配置文件”：直接打开 `openclaw.json`。
- “打开技能目录”：打开 `workspace\skills`。
- “打开数据目录”：打开整个 `openclaw-data` 文件夹。

三、模型与 API Key 配置（在应用内完成）
--------------------------------------
1. 在控制台界面进入 **设置（Config）**。
2. 根据需要选择模型提供商（如 DeepSeek / OpenAI / Anthropic / 自定义），填写：
   - API Key（密钥）
   - 模型 ID（如 `deepseek/deepseek-chat`、`openai/gpt-4o` 等）
   - 修改`openclaw-data\openclaw.json`文件中得“apiKey”的值可以直接使用deepseek ,如果需要使用彼得模型需要整体修改models中的配置
3. 保存后即可在对话中使用，无需在系统环境变量中额外配置。

四、内置 OpenClaw 与 Node 的升级
-------------------------------
本桌面应用自带：

- 内置 Node：位于 `resources\bin\node\`
- 内置 OpenClaw：位于 `resources\openclaw\`

**注意：这些是独立于系统环境的“内置版本”，不会依赖用户机器上单独安装的 Node 或 openclaw。**

当官方发布了新的 OpenClaw 版本，或需要升级内置 Node 时，可以使用本目录中的脚本：

### 1. 一键升级内置 OpenClaw 与 Node（推荐）

脚本名称：`升级内置OpenClaw环境.cmd`

使用步骤：

1. 确保 **已关闭** 所有正在运行的 `OpenClaw.exe`。
2. 在 `OpenClaw.exe` 所在目录（例如 `win-unpacked`）中，双击运行：
   - `升级内置OpenClaw环境.cmd`
3. 脚本会自动完成：
   - 关闭正在运行的 `OpenClaw.exe` 和相关 `node.exe`。
   - 下载并解压指定版本的 Node（当前为 `22.16.0`），更新到 `resources\bin\node\`。
   - 使用内置 Node 的 npm，将 `resources\openclaw\` 中的 OpenClaw 升级到最新版本。
4. 升级成功后，脚本会提示：
   - 内置 Node 版本号
   - 内置 OpenClaw 已更新位置
5. 之后直接双击 `OpenClaw.exe` 即可使用 **最新的内置 OpenClaw + Node**。

### 2. 关于 Node 版本

- 当前桌面应用内置的 OpenClaw 要求 Node 版本至少为 **22.16.0**。
- 脚本会自动下载并安装该版本到内置目录，不依赖用户机器上是否安装了 Node。
- 如将来 OpenClaw 官方提高 Node 最低版本，只需：
  - 更新脚本中 `NODE_VERSION=` 的值，并重新分发新的应用版本。

五、常见问题
------------

1. **启动很慢或一直停在“正在启动 OpenClaw…”**
   - 首次启动时，内置 Gateway 需要初始化，可能需要几十秒。
   - 若超过 3 分钟仍未进入控制台页面：
     - 打开 `openclaw-data\app-log.txt` 查看日志。
     - 检查 18789 端口是否被其他程序占用。

2. **提示“OpenClaw Gateway 启动超时（180s）”**
   - 查看提示中的日志路径和 Gateway 输出信息。
   - 若日志中出现 Node 版本不满足要求、或 OpenClaw 版本错误，建议先运行：
     - `升级内置OpenClaw环境.cmd` 进行内置环境升级。

3. **点击“检查更新”报无法检查更新 / 未配置更新源**
   - 这是桌面应用自身的“应用更新”功能：
     - 如未配置 GitHub 更新源，可能会提示“未配置更新源，请从官网下载新版本”。
   - 在未配置自动更新源的情况下，建议直接：
     - 从发布页下载新版本桌面应用，覆盖当前目录（保留 `openclaw-data`）。

4. **如何备份与迁移**
   - 备份整个 `openclaw-data` 文件夹。
   - 在新机器上，将 `openclaw-data` 与新的 `OpenClaw.exe` 所在目录放在一起，即可沿用原有配置与数据。

六、文件说明（桌面版目录）
------------------------

常见文件与目录：

- `OpenClaw.exe`：桌面应用主程序。
- `resources\bin\node\`：内置 Node 运行时。
- `resources\openclaw\`：内置 OpenClaw 运行环境。
- `openclaw-data\`：配置、工作区、日志等数据。
- `升级内置OpenClaw环境.cmd`：一键升级内置 OpenClaw 与 Node 的脚本（中文简体）。
- `使用说明-OpenClaw桌面版.txt`：本使用说明。

如遇到其它无法解决的问题，可先查看 `openclaw-data\app-log.txt` 中的详细日志信息，再联系开发者。

