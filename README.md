一个为 Windows 打包的 OpenClaw 桌面应用，目标是：**开箱即用、无需手动安装 Node / openclaw、数据完全在本地目录中可备份/迁移**。

---

## 功能概览

- **内置 OpenClaw Gateway 与 Node 运行时**（独立于系统环境）。
- 双击 `OpenClaw.exe` 即可启动，自动打开 OpenClaw 控制台 UI。
- 内置中文 UI 文案与帮助文档：
  - `assets/help.html`：应用内“帮助文档”。
  - `使用说明-OpenClaw桌面版.txt`：给最终用户的离线说明书。
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

更多高级玩法（自定义 workspace、添加自定义插件等），可参考 OpenClaw 官方文档以及本项目的 `OpenClaw-Windows-桌面应用封装-计划与报告.md`。

