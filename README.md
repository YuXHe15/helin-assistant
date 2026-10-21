# Helin Assistant 0.4.13

在 Obsidian 原文旁阅读短摘要，在后台连接已有知识、补充必要的知识页，并查看或安全撤销自动修改。支持简繁显示和摘要内公式、代码排版。

Read concise AI summaries beside your Obsidian notes. Connect related knowledge in the background, review changes, and undo them when their versions still match. Includes display-only Simplified/Traditional Chinese conversion and mathematical/code formatting.

**需要已有服务账号和 Vault 权限。** 本插件连接配套的 HTTPS 助手服务，服务入口由管理员单独提供。安装插件不会创建账号或授予笔记权限；没有账号时请联系服务管理员。本插件连接配套服务，不能单独离线生成摘要，也不在 iPad 上运行模型。

**An existing service account and access to a configured Vault are required.** The companion HTTPS assistant service is provided separately by its administrator. Installation does not create an account or grant Vault access. AI processing requires the service and its inference worker to be online.

## 功能 / Features

- **原文旁摘要**：后台生成全文与 `#` / `##` 章节摘要，优先使用简短要点或小表格。根据阅读区的可用宽度显示右侧摘要带；窄窗口在标题附近保留短预览，可展开全文。简繁切换、调整宽度与摘要更新会保留展开状态；摘要不写入 Markdown，结果须与本地已保存版本匹配。
- **知识联系**：默认优先复用已有笔记，仅在原文依据足够时补充独立知识页，并在准确位置添加 `[[链接]]`。新页默认与原笔记同目录，保留来源；允许不提取，不递归拆分生成页。
- **查看变更与撤销**：自动知识维护默认关闭，需明确开启；开启后按保存的目录和权限后台写入，无需逐条确认。可查看每批 diff 和修改前后全文。撤销会核对版本，保留后续已修改或被引用的知识页，可能显示部分撤销。
- **简繁显示**：角落的“简 / 繁”按钮只转换阅读视图、Live Preview 与 AI 摘要的显示，记住本设备、本 Vault 的选择。代码、公式、属性、链接目标及原文件保持原样；Live Preview 当前编辑行显示原文。
- **公式与代码**：摘要支持 `$…$`、`$$…$$`、`\(…\)`、`\[…\]`、行内代码及代码围栏。使用 Obsidian 自带 MathJax 和已加载的 Prism 语法；不执行代码、HTML、嵌入或第三方代码块处理器。无法排版时保留文字，长行可横向滚动。可运行“预览 AI 栏公式与代码”。
- **历史与归档**：支持服务提供的分页对话历史、归档与恢复；归档保留消息，关闭标签只隐藏标签。自动修改历史可继续加载更早批次，并按源笔记路径筛选。后台设置显示任务状态、错误与知识索引进度，刷新状态不会清空未保存输入。
- **搜索与 DAG**：在授权 Vault 内搜索、按行阅读、核对来源，并根据明确段落生成 DAG。DAG 写入仍需审阅并确认。没有向量索引或语义搜索。

Summary layouts follow the available reading-pane width. Narrow views retain a short preview, and expansion survives script and layout changes. History supports pagination and reversible archiving when offered by the service; closing a tab only hides it. Background status and errors refresh without discarding unsaved settings.

Background automation produces whole-note and section summaries without changing the source file. Knowledge maintenance reuses existing pages first, creates new pages only when justified by the source, and adds contextual wiki links. It is opt-in and can write in the configured scope automatically. Review every batch and use version-checked undo; edited or referenced knowledge pages may be retained. Simplified/Traditional conversion changes rendering only. Formula and code rendering never executes notebook code or third-party Markdown processors.

## 配对与会话 / Pairing and sessions

服务支持时，新版会保留设备、用户、Vault、本机绑定和服务地址，自动将已有配对升级为轮换会话，无需先退出。访问凭证有效15分钟并自动刷新；刷新凭证每次使用后轮换，闲置30天过期，会话最迟90天后需重新配对。设置中可查看到期信息。后台摘要使用同一刷新机制；断网或安全存储写入暂时失败可重试，退出会立即清除本机显示数据并尝试撤销服务端连接。无法联网时，可稍后通过门户撤销该设备。

When supported by the service, this version upgrades an existing pairing in place. Access credentials last 15 minutes and refresh automatically. Refresh credentials rotate after use, expire after 30 idle days, and have a fixed 90-day session deadline. The existing user, Vault, device and service origin are preserved. Recovery handles interrupted responses and storage failures; logout clears local state and attempts server revocation. An offline device can also be revoked through the portal.

## 从旧试用版迁移 / Migration from earlier trials

本发行的标识是 `helin-assistant`，安装仓库是 `YuXHe15/helin-assistant`。此前本项目的私有试用版 **Vault Assistant** 来自 `YuXHe15/obsidian-vault-assistant`，使用旧标识 `vault-assistant`；临时品牌 **Heyux Assistant 0.4.6** 来自 `YuXHe15/heyux-assistant`，使用标识 `heyux-assistant`。

如已安装其中任一版本，先在 Obsidian 中**停用旧私有试用插件或临时 Heyux Assistant 0.4.6**，再安装并启用 **Helin Assistant**。保留旧插件的本机配置、配对和简繁偏好供迁移使用；不要选择退出、注销或撤销旧配对，也不要删除 Markdown 笔记。新插件若提示配对，使用本人的服务账号并确认同一个远端 Vault；不要复制别人的 `data.json` 或秘密存储。迁移期间不要同时启用新旧插件。

旧 Vault Assistant 与临时 Heyux Assistant 的 BRAT 仓库均不会通过更换插件 ID 的升级改装为 Helin Assistant。请在 BRAT 中添加新仓库 `YuXHe15/helin-assistant`。

Disable either earlier trial—**Vault Assistant** or temporary **Heyux Assistant 0.4.6**—before installing **Helin Assistant**. Keep its local configuration, pairing and Simplified/Traditional display preference; do not sign out, revoke the old pairing, or delete notes. If pairing is requested, use your own service account and the same remote Vault. Do not copy another person's configuration or secrets. Add the new repository in BRAT; neither earlier repository will be upgraded to a different plugin ID. Keep only one of these plugins enabled.

## 安装与设备 / Installation and devices

最低 Obsidian 版本：**1.11.4**。首版移动支持目标包含 **iPadOS**。实体 iPad 的浏览器配对返回、软键盘、分屏、触控与恢复连接尚未完成验收；iPhone 和 Android 也尚未完成实体设备验收。桌面已有验收不代表这些移动流程已经通过。请在目标设备验证后再用于重要资料。

Minimum Obsidian version: **1.11.4**. **iPadOS is a mobile release target; physical-device validation is still pending**, including pairing return, software keyboard, split view, touch and reconnection. iPhone and Android hardware have not been validated either. Desktop validation and automated tests do not establish mobile compatibility.

社区目录是否已收录、哪个版本可安装，以 [Obsidian 社区目录](https://community.obsidian.md/plugins) 实际显示为准。本说明与本地构建不代表审核已经通过。

Before installing version **0.4.13**, verify that its matching [GitHub release](https://github.com/YuXHe15/helin-assistant/releases) exists. These instructions do not claim that this version has already been published or accepted into the community directory.

- **社区目录 / Community directory**：收录后，在 Obsidian 的第三方插件浏览中搜索 **Helin Assistant**，安装并启用。
- **试用 / BRAT**：安装 [BRAT](https://github.com/TfTHacker/obsidian42-brat)，添加 `YuXHe15/helin-assistant`，选择已发布的目标版本，再启用 Helin Assistant。普通安装不需要 GitHub 令牌。
- **桌面手动安装 / Desktop manual installation**：下载同版本 `helin-assistant-0.4.13.zip`，将其中的 `helin-assistant` 文件夹放到 Vault 的 `.obsidian/plugins/`。更新时替换发布文件，保留已有本机配置与配对。

安装目录内的运行文件是 `manifest.json`、`main.js` 和 `styles.css`。保留随包附带的 `LICENSE`、`COPYRIGHT.txt` 和 `THIRD_PARTY_NOTICES.txt`；许可证也附在 `main.js` 中，覆盖只下载运行文件的安装方式。不要复制他人的 `data.json` 或秘密存储。

## 首次使用 / Getting started

1. 使用管理员单独提供的服务门户登录，确认账号与目标 Vault 已开通助手。
2. 在 Obsidian 命令面板运行 **Helin Assistant: 打开搜索助手**。首次使用先填写管理员提供的 HTTPS 服务地址，再选择 **开始配对**；安装包不内置服务域名。已有设备保留原先保存的地址和配对。
3. 在系统浏览器登录，核对两边的配对码，选择对应的远端 Vault 后授权，再返回 Obsidian。每个本地 Vault、每台设备独立配对。
4. 核对面板中的用户、Vault 与只读状态。搜索阅读可保持只读；DAG 写入需要关闭只读并确认差异。
5. 如需后台整理，打开 **配置自动摘要与知识网络**，选择源目录并分别开启摘要、知识维护。留空源目录表示授权范围内整个 Vault；默认静置 120 秒后进入队列。通过 **查看自动概念变更与撤销** 核对写入。

Sign in to the service portal first. Open **Helin Assistant** from Obsidian's command palette, enter the administrator-provided HTTPS service address on first setup, then start pairing, verify the code in both places, authorize the correct remote Vault in the browser, and return to Obsidian. Enable background summaries and knowledge maintenance separately if wanted. The service, synchronized Vault copy and Mac inference worker must remain available; closing Obsidian does not stop an already enabled background queue.

## 网络、数据与隐私 / Network, data and privacy

- **远端服务**：插件通过 HTTPS 连接配套助手服务，完成登录配对、任务、会话、摘要、变更历史和授权操作。已有服务账号与 Vault 权限是完整功能的前提。
- **发送内容**：问题、选择的对话上下文、明确选择的段落、笔记路径、行号及版本摘要会按请求发给该服务。主动基于笔记绘图时，会读取选定笔记核对版本并上传相关选段。后台生成读取服务端已经同步且已授权的笔记副本；不是把当前设备所有文件直接上传给模型。
- **处理与保存**：服务端及运营者的 Mac 推理 worker 处理授权材料，使用配套的 Qwen 模型。服务会保存账号/设备授权、对话、任务、派生摘要和自动修改记录，以提供历史与撤销。使用者应只授权可交给该服务处理的 Vault。
- **本机数据**：配对令牌存于 Obsidian SecretStorage；连接引用、显示偏好和聊天标签标识保存在本机配置。简繁转换的 OpenCC 字典随包提供，离线转换，不调用翻译服务。摘要和简繁切换均不改写原 Markdown。
- **无客户端遥测**：插件不收集客户端分析、使用统计或广告追踪，不发送遥测。为提供功能而请求会话、摘要和任务接口不属于客户端遥测。服务端会保存上述功能数据；不要把“无客户端遥测”理解成服务不保存对话。
- **GitHub / BRAT**：用于分发和更新插件文件，插件不向 GitHub 上传笔记、聊天或凭据。普通来源链接只打开本地 Vault 中已有文件；点击外部资料链接会交由系统处理。

The plugin connects to the configured companion HTTPS service for pairing and authorized assistant features. Questions, selected context/passages, note paths, line numbers and content-version hashes are sent as needed. Background processing reads the service's authorized synchronized Vault copy. The service and its Mac worker process that data and store conversations, jobs, derived summaries and change history for the advertised functions. Tokens use Obsidian SecretStorage. **There is no client-side telemetry, analytics or advertising tracking.** OpenCC conversion is local; notes and credentials are not uploaded to GitHub. GitHub and BRAT distribute installation files. Obsidian plugins share application privileges; enable plugins only in a trusted environment.

## 许可与分发 / License and distribution

第一方插件为闭源软件，下载、安装与已授权服务配合使用的许可见 [LICENSE](LICENSE)。版权声明见 [COPYRIGHT.txt](COPYRIGHT.txt)。未授予第一方代码的开源、修改或公开再分发许可。第三方组件继续适用各自许可，完整条款见 [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt)，并附在 `main.js` 中。

The first-party plugin is proprietary. [LICENSE](LICENSE) permits downloading, installation and use with authorized service access; it does not grant an open-source license. Third-party components retain their own licenses. The installation repository contains release files and documentation, not the service infrastructure or private development source. Plugin source can be supplied through the community directory's private-source review mechanism without publishing the backend. `SHA256SUMS` covers the supplied release files.

## 源码审核构建 / Source-review build

以下命令用于插件开发/审核源码仓库，不适用于只有安装文件的公开分发仓库。Node.js 20+ 与 pnpm：

```sh
pnpm install --frozen-lockfile --ignore-scripts
pnpm build
pnpm test
```

构建只生成插件文件，不安装到 Vault、不发布 GitHub Release，也不提交社区目录。
