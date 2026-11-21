# dsh-thinking-zh

在 DSH 对话中阅读中文的模型思考内容，随时可切回原文。

## 安装

本插件是 DSH bundle，只通过 GitHub 仓库分发，不发布到 npm：

1. 克隆仓库：

   ```bash
   git clone https://github.com/filek-mu/dsh-thinking-zh.git
   ```

2. 在 DSH 的「插件」页点「添加插件」，选择克隆下来的目录；或者用 `plugin_manager` 的 `install_bundle` 传入该目录的绝对路径。
3. 启用「思考中文翻译」，保持它的两个子项同时启用，刷新页面后展开任意思考内容。

在 DSH `0.2.2-rc.5` 上验证。插件挂载的是 DSH 自带的实验性翻译包，升级 DSH 后行为可能变化。

> 注意：npm 上另有一个同名的 `dsh-thinking-zh`（作者 minutiae3），与本项目无关。请从本仓库以本地目录方式安装，不要执行 `npm install dsh-thinking-zh`。

## 中文

- **作用**：把展开的模型思考内容显示为简体中文。展开思考行后，已完成的段落会自动换成中文；工具栏可在“查看原文”和“查看译文”之间切换。首批译文返回前，正文仍显示原文。
- **控制**：“查看原文”只切换显示，不会取消已经发出的翻译请求；要停止请求请收起思考行或停用插件。
- **原文保留**：Session 记录、模型上下文和折叠摘要都保持原文；机器翻译可能改变 Markdown 或代码格式。
- **隐私**：展开的思考正文会经 Host 发送到 Bing 匿名翻译接口，可能含代码和对话细节；不使用 Google，不需要登录凭据。
- **网络**：Bing 匿名接口不保证可用；失败时正文保留原文并提供重试。
- **停用**：在插件页面停用「思考中文翻译」即可移除控件并取消待处理请求。插件页里的两个子项（翻译服务、思考翻译）需要同时保持启用，也不要同时启用官方「思考过程机器翻译」，两者使用同一组插件行。

## English

Translate expanded model reasoning into Simplified Chinese inside DSH Chat.

### Install

This is a DSH bundle distributed from this repository only; it is not published to npm.

1. Clone the repository:

   ```bash
   git clone https://github.com/filek-mu/dsh-thinking-zh.git
   ```

2. In DSH, open **Plugins** → **Add plugin** and choose the cloned directory, or pass its absolute path to `plugin_manager` `install_bundle`.
3. Enable **Reasoning in Chinese**, keep both of its rows enabled, and refresh the page.

Tested with DSH `0.2.2-rc.5`. It mounts the experimental translator packages shipped with DSH, so behavior may change after a DSH upgrade.

> Note: an unrelated npm package named `dsh-thinking-zh` exists. Install this bundle from a local clone, not with `npm install dsh-thinking-zh`.

### What it does

The bundle mounts the reasoning translator that ships with DSH and fixes its defaults to Simplified Chinese:

- Provider: Bing anonymous translation endpoint.
- Target language: `zh` (Simplified Chinese).
- Text translated: the reasoning body of an expanded thinking block.
- Original text: the Session log, the model context, and the collapsed preview keep the original wording.

### How to use

1. Expand a thinking block in Chat. Completed paragraphs are replaced with Simplified Chinese automatically; before the first translation arrives the body still shows the original.
2. The toolbar above the reasoning body switches between **View original** and **View translation**. The running tail of a streaming paragraph stays in the original language until that paragraph completes. Viewing the original only changes the display; requests already in flight continue. Collapse the block or disable the plugin to cancel pending requests.
3. If a request fails, the body keeps the original text and offers **Retry**; nothing is switched to another service automatically.

The bundle inserts two rows (translation service and reasoning translation); keep both enabled. Do not enable the official “reasoning translation” bundle alongside this one: it uses the same rows.

Finished paragraphs, and the finished prefix of a long streaming paragraph, are translated as they become available. Collapsing the block or disabling the plugin cancels pending requests. Successful translations are stored in the Session and reused after re-expanding, reloading, or restarting the Host.

### Privacy and network

The text of an expanded reasoning block is sent to Microsoft's anonymous Bing translation endpoint through the DSH Host. It may contain private code or conversation details. Google is not used here; Bing is the only configured provider. Bing and other anonymous endpoints are not guaranteed to be available or free, and availability in mainland China depends on your network. No translation service receives credentials.

### Limitations

- Only the expanded body is translated. The collapsed reasoning summary keeps its original language.
- Machine translation may alter Markdown formatting or code samples; the original is always one click away.
- Reasoning in subagent Sessions without a saved translation may stay in the original language.
- The plugin wraps the experimental translator packages shipped with DSH; DSH upgrades may change them.

### Turn it off

Disable **Reasoning in Chinese** on the Plugins page. The reasoning toolbar disappears and pending requests are cancelled; stored translations remain in the Session log.
