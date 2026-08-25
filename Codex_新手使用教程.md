# minicamp 2026 · Codex 新手使用教程

本教程为MINICAMP团队成员创作，转载请注明出处 作者：**LHC-PROG**  

**Windows / macOS / Linux · 按系统与使用基础分流**
 
<a id="toc"></a>
## 目录

> 建议首次阅读时按顺序先完成 **[第 1 章通用准备](#common-start)**，再进入“快速定位”。目录用于查找内容，不建议直接跳过通用前置步骤。

- [第 1 章　网络、账号与最小准备](#common-start)
  - [1.2 没有 ChatGPT 账号怎么办？](#account-signup)
  - [1.3 免费账号能不能用 Codex？](#free-plan)
- [快速定位：先选操作系统，再选自己的情况](#quick-start)
- [第 2 章　Windows 用户](#windows)
  - [2.1 完全不会编程：ChatGPT 官方桌面端](#windows-no-code)
  - [2.2 有编程基础且已有 VS Code：官方 Codex 扩展](#windows-vscode-user)
  - [2.3 有编程基础但没有 VS Code：VS Code 或 CLI](#windows-no-vscode)
- [第 3 章　macOS 用户](#macos)
  - [3.1 完全不会编程：ChatGPT 官方桌面端](#macos-no-code)
  - [3.2 有编程基础且已有 VS Code：官方 Codex 扩展](#macos-vscode-user)
  - [3.3 有编程基础但没有 VS Code：VS Code 或 CLI](#macos-no-vscode)
- [第 4 章　Linux 用户](#linux)
  - [4.1 Linux 桌面端支持范围](#linux-desktop-support)
  - [4.2 完全不会编程：桌面端或 VS Code](#linux-no-code)
  - [4.3 有编程基础且已有 VS Code：官方 Codex 扩展](#linux-vscode-user)
  - [4.4 有编程基础但没有 VS Code：VS Code 或 CLI](#linux-no-vscode)
- [第 5 章　统一练习：网页番茄钟（选做）](#unified-practice)
- [第 6 章　看懂 Codex：读取、修改、命令与权限](#codex-basics)
- [第 7 章　第一次 Debug：出错以后怎么做](#debug)
- [第 8 章　minicamp 常用 Prompt 模板](#prompt-templates)
- [第 9 章　赛前验收：做到这些就够了](#preflight)
- [常见问题 Q&A](#faq)
- [附录 A　官方资料与版本说明](#appendix-a)

---

> **第 1 步：完成 [第 1 章：网络、账号与最小准备](#common-start)。这一章建议不要跳过。**  
> 第 2 步：完成账号检查点并创建练习文件夹后，再进入 [快速定位](#quick-start)。  
> 第 3 步：先选自己的操作系统，再根据“是否会编程、是否已有 VS Code、是否习惯终端”进入对应路线。  
> 第 4 步：任一 Codex 入口跑通后，再继续到第 5 章“统一练习”。

> **这份教程只假设一件事**
>
> 你的电脑已经有可用网络环境，可以正常访问 ChatGPT。即使你没有 ChatGPT 账号、完全不会编程、不懂终端、也没有安装 VS Code，都可以按对应路线从头开始。

> **特别说明**
>
> 如果你觉得教程中的某些步骤还不够详细，或者在实际操作时遇到了没有覆盖的问题，可以先尝试把问题交给 AI，很多安装、报错和使用上的小问题都可以直接向它询问。
>
> 如果问题还是没有解决，也欢迎随时联系我们。教程难免有疏漏，我们也会根据大家遇到的问题不断补充和完善，感谢你的反馈！


*Meet. Build. Make Something Together.*

Codex · 新手使用教程 · v1.6 · 2026-08-22

<a id="common-start"></a>
# 第 1 章　网络、账号与最小准备

## 1.1 网络检查

1. 打开浏览器。

2. 访问 <https://chatgpt.com/>。

3. 页面能正常加载后再继续。

本教程不讲代理软件、节点、TUN 模式或系统代理配置；这些属于赛前基础环境。

<a id="account-signup"></a>
## 1.2 没有 ChatGPT 账号怎么办？

1. 打开 <https://chatgpt.com/>。

2. 选择注册（Sign up）。

3. 按页面提示创建账号；可以使用页面提供的邮箱或第三方账号登录方式。

4. 注册完成后，先发送一条普通 ChatGPT 消息，确认账号可正常使用。

<a id="free-plan"></a>
## 1.3 免费账号能不能用 Codex？

按 2026-08-22 核对的 OpenAI 官方帮助说明，Codex 已包含在 Free、Go、Plus、Pro、Business、Edu 和 Enterprise 等 ChatGPT 方案中，但不同方案的使用额度不同。不要因为没有 Plus 就先放弃；先用自己的账号登录实际检查可用额度。

> **账号检查点**
>
> □ chatgpt.com 能打开
>
> □ 能登录自己的账号　
>
> □ 能发送普通 ChatGPT 消息

## 1.4 先建一个统一练习文件夹

为了让三种系统和三种入口使用同一套练习，请先在你容易找到的位置新建文件夹：

```text
minicamp-codex-demo
```

后面所有“打开项目”“打开文件夹”“进入目录”，都指这个文件夹。



<a id="quick-start"></a>
# 快速定位：先选操作系统，再选自己的情况

> **进入本节前，请先确认**
>
> 你已经完成 [第 1 章](#common-start)：能打开 ChatGPT、能登录账号，并已经创建 `minicamp-codex-demo` 文件夹。

接下来就可以先按照电脑的操作系统进行分流，进入自己的系统后，再判断自己属于下面哪一种情况。

| **情况** | **建议入口** | **原因** |
|---|---|---|
| **完全不会编程** | **官方 ChatGPT 桌面端中的 Codex** | 安装步骤少，不需要先理解 IDE、Git 或终端，适合先把完整体验跑通 |
| **有编程基础，而且已经有 VS Code** | **VS Code + OpenAI 官方 Codex 扩展** | 可以直接在熟悉的编辑器里读代码、看差异、继续修改 |
| **有编程基础，但没有 VS Code，且习惯终端** | **Codex CLI** | 不必为了 Codex 额外安装 VS Code，直接在项目目录工作 |
| **有编程基础，但没有 VS Code，也不习惯终端** | **安装 VS Code + 官方 Codex 扩展** | 比直接学习 CLI 更直观，后续参加 Hackathon 也更方便查看代码 |

> **Linux 有一个例外**
>
> ChatGPT Linux 桌面端目前仍是 Preview，并只正式支持部分 Ubuntu / Debian / Fedora 桌面版本。因此 Linux 完全零基础用户先检查发行版：**受支持 → 优先桌面端；不受支持 → 使用 VS Code + Codex 扩展。**

## 直接进入你的系统

- [**Windows 用户 → 第 2 章**](#windows)
- [**macOS 用户 → 第 3 章**](#macos)
- [**Linux 用户 → 第 4 章**](#linux)

> **三种入口互相独立**
>
> 使用 VS Code 官方 Codex 扩展，不需要先安装 Codex CLI；使用 ChatGPT 桌面端，也不需要先安装 CLI。只有你主动选择终端路线时，才需要安装 Codex CLI。


<a id="windows"></a>
# 第 2 章　Windows 用户

> 如果你不确定自己该选哪一条，按顺序看下面三个入口即可。我们尽量让你只安装真正需要的工具。

<a id="windows-no-code"></a>
## 2.1 完全不会编程：优先使用 ChatGPT 官方桌面端

> **适合你，如果：**你几乎没有写代码经验，也不熟悉 VS Code、Git 或 PowerShell。

这条路线的目标很简单：先用图形界面把 Codex 跑起来，不要求你为了“学 AI Coding”先学一整套开发工具。

### 2.1.1 安装 ChatGPT 官方 Windows 应用

你可以从下面任一官方入口开始：

- [ChatGPT 官方下载页](https://chatgpt.com/download/) → 选择 Windows；
- 或在 Microsoft Store 中安装官方 ChatGPT 应用，并确认发布者为 OpenAI。

如果从官方 Windows 文档进入，最终也会进入微软官方分发渠道。

安装完成后打开 ChatGPT，并登录你在 [第 1 章](#common-start) 准备好的账号。

### 2.1.2 进入 Codex，并打开练习项目

1. 在 ChatGPT 桌面应用中完成登录并进入 Codex。
2. 选择打开本地项目 / 文件夹。
3. 选择 `minicamp-codex-demo`。
4. 发送：

```text
先查看当前项目，不要修改任何文件。
告诉我这里目前有什么，以及如果我要做一个最简单的网页 Demo，下一步应该先做什么。
```

如果 Codex 能识别这个目录，你已经完成最重要的准备。

> **给零基础同学的一点说明**
>
> 比赛过程中如果你逐渐需要自己查看和调整代码，再安装 VS Code 也完全来得及。现在先把 Codex 用起来即可，不必一次把所有工具都装齐。

[**→ 已跑通：进入第 5 章统一练习**](#unified-practice)

<a id="windows-vscode-user"></a>
## 2.2 有编程基础，并且已经有 VS Code：安装官方 Codex 扩展

> **适合你，如果：**平时已经使用 VS Code 写代码，希望 Codex 直接出现在编辑器旁边。

1. 打开 VS Code。
2. 点击左侧 **Extensions（扩展）**。
3. 搜索 `Codex`。
4. 确认是 **OpenAI 官方 Codex 扩展**，发布者为 **OpenAI**。
5. 点击 **Install**。
6. 如果安装后没有看到 Codex 图标，按 `Ctrl + Shift + P`，运行：

```text
Codex: Open Codex Sidebar
```

> **这里不需要做的事**
>
> 不需要 `npm install -g @openai/codex`；不需要先安装 Codex CLI；也不需要为了 VS Code 扩展单独安装 Node.js。

### 登录并打开项目

1. 在 Codex 面板按提示登录 ChatGPT 账号。**最好先在默认浏览器中登录好自己的 ChatGPT 账号，这样 Codex 弹出浏览器授权页面时通常会更顺畅。**
2. `File → Open Folder`，选择 `minicamp-codex-demo`。
3. 打开 Codex 侧边栏发送：

```text
先查看当前工作区，不要修改任何文件，告诉我这里有什么。
```

如果 Codex 能说出当前工作区为空或列出已有文件，这条路线就已经跑通。Codex 侧边栏的入口通常位于 VS Code 界面的右上角。

如果没有看到 Codex 侧边栏入口，可能是当前工作区处于受限模式。请根据 VS Code 的提示将工作区设为受信任状态后再尝试。

[**→ 已跑通：进入第 5 章统一练习**](#unified-practice)

<a id="windows-no-vscode"></a>
## 2.3 有编程基础，但没有 VS Code：按是否习惯终端选择

### 情况 A：你习惯 PowerShell / Terminal

可以直接使用 Codex CLI，不必为了 Codex 单独安装 VS Code。

Windows 如果使用 npm 安装路线，需要先有 Node.js/npm：

1. 从 <https://nodejs.org/> 安装当前 LTS 版本。
2. 重新打开 PowerShell。
3. 检查：

```powershell
node --version
npm --version
```

4. 安装 Codex CLI：

```powershell
npm i -g @openai/codex
codex --version
```

5. 进入练习目录后运行：

```powershell
cd <你的 minicamp-codex-demo 路径>
codex
```

第一次启动按提示选择使用 ChatGPT 账号登录。

### 情况 B：你会编程，但平时不习惯终端

建议安装 VS Code，再走 [2.2 VS Code + 官方 Codex 扩展](#windows-vscode-user)。这样比赛时查看文件、修改差异和运行结果会更直观。

> **Windows 完成标志**
>
> ChatGPT 桌面端 / VS Code 扩展 / Codex CLI 至少一种可用，并且 Codex 能读取 `minicamp-codex-demo`。

[↩ 返回“快速定位”](#quick-start)　·　[↑ 返回目录](#toc)


<a id="macos"></a>
# 第 3 章　macOS 用户

<a id="macos-no-code"></a>
## 3.1 完全不会编程：优先使用 ChatGPT 官方桌面端

> **适合你，如果：**你希望尽量少接触终端和开发环境，先用图形界面完成第一次 Codex 体验。

1. 打开 [ChatGPT 官方下载页](https://chatgpt.com/download/)。
2. 下载并安装 macOS 版 ChatGPT。
3. 登录自己的 ChatGPT 账号。
4. 进入 Codex。
5. 打开 `minicamp-codex-demo`。
6. 发送：

```text
先查看当前项目，不要修改任何文件。
告诉我这里目前有什么，以及如果我要做一个最简单的网页 Demo，下一步应该先做什么。
```

如果 Codex 能识别这个项目目录，就可以继续统一练习。

[**→ 已跑通：进入第 5 章统一练习**](#unified-practice)

<a id="macos-vscode-user"></a>
## 3.2 有编程基础，并且已经有 VS Code：安装官方 Codex 扩展

1. 打开 VS Code。
2. 在扩展商店搜索 `Codex`。
3. 确认发布者为 **OpenAI**。
4. 安装扩展并打开 Codex 侧边栏。
5. 使用 ChatGPT 账号登录。
6. `File → Open Folder` → 选择 `minicamp-codex-demo`。

> **提醒**
>
> VS Code Codex 扩展是独立入口，不需要先安装 Codex CLI，也不需要为了这个扩展单独安装 Node.js。

建议先发送：

```text
先查看当前工作区，不要修改任何文件，告诉我这里有什么。
```

[**→ 已跑通：进入第 5 章统一练习**](#unified-practice)

<a id="macos-no-vscode"></a>
## 3.3 有编程基础，但没有 VS Code：按是否习惯终端选择

### 情况 A：习惯 Terminal

可以直接安装 Codex CLI。macOS 当前可使用 OpenAI 官方独立安装器，不需要为了 Codex CLI 单独安装 Node.js：

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

按提示刷新 Shell 或重新打开终端，然后：

```bash
codex --version
cd /path/to/minicamp-codex-demo
codex
```

第一次运行时选择 `Sign in with ChatGPT`。

### 情况 B：会编程，但不习惯终端

建议先安装 [VS Code](https://code.visualstudio.com/)，再按照 [3.2](#macos-vscode-user) 安装官方 Codex 扩展。

> **macOS 完成标志**
>
> ChatGPT 桌面端 / VS Code 扩展 / Codex CLI 至少一种可用，并且 Codex 能读取 `minicamp-codex-demo`。

[↩ 返回“快速定位”](#quick-start)　·　[↑ 返回目录](#toc)


<a id="linux"></a>
# 第 4 章　Linux 用户

> Linux 的分流和 Windows / macOS 基本一致，只是“完全不会编程”这条路线需要先确认你的发行版是否在 ChatGPT Linux 桌面端的官方支持范围内。

<a id="linux-desktop-support"></a>
## 4.1 先确认 Linux 桌面端支持范围

截至 2026-08-22，ChatGPT Linux 桌面应用仍是 Preview。OpenAI 当前正式支持以下桌面发行版：

- Ubuntu 24.04 LTS / 26.04 LTS
- Debian 13
- Fedora 43 / 44

并提供 x64 与 ARM64 安装包。可以用下面的命令检查架构：

```bash
uname -m
```

`x86_64` = x64；`aarch64` / `arm64` = ARM64。

其他发行版有可能运行，但不属于当前官方正式支持范围。

<a id="linux-no-code"></a>
## 4.2 完全不会编程：先看发行版，再选桌面端或 VS Code

### 情况 A：你的发行版在官方支持范围内

优先使用 ChatGPT Linux 桌面端 Preview。这样不需要先学习 Codex CLI。

从官方 Linux 文档下载与你发行版、处理器架构匹配的 `.deb` 或 `.rpm` 包：

[OpenAI Linux 桌面端官方文档](https://learn.chatgpt.com/docs/linux/linux-app)

Ubuntu / Debian 示例（文件名以实际下载文件为准）：

```bash
cd ~/Downloads
sudo apt install ./chatgpt_amd64.deb
```

Fedora 示例：

```bash
cd ~/Downloads
sudo dnf install ./chatgpt.x86_64.rpm
```

安装后从应用菜单启动 ChatGPT，登录账号，进入 Codex，并打开 `minicamp-codex-demo`。

> 如果你对上面的安装命令不熟悉，不必勉强自己理解每个参数。可以请现场 Mentor 协助确认下载文件名和安装步骤。

### 情况 B：你的发行版不在官方支持范围内

不建议为了入门 Codex 去折腾不受支持的桌面端，也不建议完全零基础时直接学习 CLI。更稳妥的方式是安装 VS Code，再使用官方 Codex 扩展：

1. 安装适合你发行版的 VS Code。
2. 在扩展商店搜索 `Codex`。
3. 确认发布者为 OpenAI。
4. 安装并登录 ChatGPT 账号。
5. 打开 `minicamp-codex-demo`。

[**→ 已跑通：进入第 5 章统一练习**](#unified-practice)

<a id="linux-vscode-user"></a>
## 4.3 有编程基础，并且已经有 VS Code：安装官方 Codex 扩展

1. 打开 VS Code。
2. 在扩展商店搜索 `Codex`。
3. 确认发布者为 OpenAI。
4. 安装扩展并打开 Codex 侧边栏。
5. 使用 ChatGPT 账号登录。
6. 打开 `minicamp-codex-demo`。

> VS Code Codex 扩展不需要先安装 Codex CLI。

[**→ 已跑通：进入第 5 章统一练习**](#unified-practice)

<a id="linux-no-vscode"></a>
## 4.4 有编程基础，但没有 VS Code：按是否习惯终端选择

### 情况 A：习惯终端

可以直接使用 Codex CLI。Linux 当前可使用 OpenAI 官方独立安装脚本，因此不需要为了 Codex CLI 额外安装 Node.js：

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

安装后按提示刷新 Shell，然后：

```bash
codex --version
cd ~/path/to/minicamp-codex-demo
codex
```

第一次启动选择 `Sign in with ChatGPT`。

### 情况 B：会编程，但不习惯终端

建议安装 VS Code，再按照 [4.3](#linux-vscode-user) 使用官方 Codex 扩展。

### Wayland 注意事项

OpenAI 当前说明原生 Wayland 支持仍在改进。默认先正常启动应用；只有确实遇到兼容问题并知道自己在做什么时，再尝试：

```bash
chatgpt --ozone-platform=wayland
```

比赛前不必为了窗口效果反复调整 Wayland；稳定可用更重要。

> **Linux 完成标志**
>
> ChatGPT Linux 桌面端 Preview / VS Code 扩展 / Codex CLI 至少一种可用，并且 Codex 能读取 `minicamp-codex-demo`。

[↩ 返回“快速定位”](#quick-start)　·　[↑ 返回目录](#toc)

<a id="unified-practice"></a>
# 第 5 章　所有路线汇合：用 Codex 做第一个网页番茄钟
（选做。本练习会占用一定的 Codex 使用额度，可根据自己的账号额度和兴趣自行选择是否完成。）

> **进入本章前必须同时满足两件事**
>
> 1. 已完成 [第 1 章：网络、账号与最小准备](#common-start)；  
> 2. 已按 [快速定位](#quick-start) 跑通至少一种 Codex 入口，并确认它能读取 `minicamp-codex-demo`。  
> 如果任一条件没有满足，请不要从外部链接直接从本章开始。

> **从这里开始，Windows / macOS / Linux 完全通用**
>
> 你只需要在自己已经跑通的 Codex 入口里发送下面的 Prompt。无论是 VS Code 扩展、桌面端还是 CLI，目标都一样。

## 5.1 最终目标

- 25 分钟倒计时

- 开始 / 暂停 / 重置按钮

- 一个简单任务输入框

- 清晰、可演示的页面布局

- 只用原生 HTML + CSS + JavaScript，不引入复杂框架

## 5.2 第一步：先让 Codex 规划

```text
请先查看当前项目目录，不要马上写代码。
我要做一个简单的网页版番茄钟：25 分钟倒计时、开始/暂停/重置按钮、一个任务输入框。
请先告诉我准备创建哪些文件、每个文件负责什么，以及最小可行实现步骤。
```

重点不是“让 AI 一句话生成全部”，而是先知道它打算怎么做。

## 5.3 第二步：确认后再实现

```text
这个计划可以。请按最小可行版本开始实现。
完成后告诉我你创建/修改了哪些文件，以及我应该怎样在浏览器中验证。
```

完成后自己确认项目目录里真的出现了文件。

## 5.4 第三步：打开 Demo

1. 在项目目录找到 index.html。

2. 双击，用浏览器打开。

3. 测试开始、暂停、重置。

4. 输入一条任务，确认页面交互正常。

## 5.5 第四步：做一次自然语言迭代

```text
保持现有功能不变，把页面做得更简洁、更适合现场展示。
让倒计时数字更醒目，按钮间距更合理，并给当前任务增加一个清晰区域。
修改后请告诉我具体改了什么。
```

## 5.6 第五步：让 Codex 同时当“临时老师”

```text
我对前端不熟。请用小白能听懂的方式解释 index.html、CSS 和 JavaScript 各自负责什么；
只解释这个项目真正用到的部分，不要展开成完整课程。
```

> **你已经完成codex新手使用教程的核心体验**
>
> 能读项目 → 能规划 → 能改文件 → 能看到 Demo → 能继续修改。接下来只需要学会看权限和 Debug。

[↩ 返回“快速定位”](#quick-start)　·　[↑ 返回目录](#toc)

<a id="codex-basics"></a>
# 第 6 章　看懂 Codex：读取、修改、命令与权限

## 6.1 Read / 读取

Codex 会读取目录结构、文件和你当前打开/选中的代码来理解项目。读取本身不会修改项目。

## 6.2 Edit / 修改

Codex 可以新建或修改文件。VS Code 里通常最容易查看差异；无论使用哪种入口，都不要只看“它说完成了”，还要看实际文件和运行结果。

## 6.3 Run / 运行命令

为了安装依赖、运行测试、启动开发服务器或检查结果，Codex 可能运行命令。新手看到命令时，先问自己：这条命令和当前任务有没有关系？

## 6.4 Approval / 权限确认

- 它准备执行什么？

- 为什么这一步和当前任务有关？

- 它会不会访问项目文件夹以外的位置？

- 它会不会删除大量文件？

- 它是否准备运行你完全不理解的高风险命令？

> **不要无脑允许**
>
> AI Coding 的正确姿势不是“所有确认都点允许”，而是让 AI 工作，同时保留你对文件、命令和最终结果的判断。

## 6.5 备份：不会 Git 也要会最简单的兜底

如果你完全不会 Git，大改之前至少复制整个项目文件夹，命名为 minicamp-codex-demo_backup。会 Git 的同学优先用 commit/checkpoint。

[↩ 返回“快速定位”](#quick-start)　·　[↑ 返回目录](#toc)

<a id="debug"></a>
# 第 7 章　第一次 Debug：出错以后怎么做

AI 生成的代码也会报错。真正有用的 AI Coding 工作流不是“一次成功”，而是快速读错误 → 定位原因 → 最小修复 → 再验证。

## 7.1 最简单 Debug Prompt

```text
当前程序出现问题。请先不要大范围重写。
请读取相关文件和错误信息，先解释最可能的原因，再做最小修改；
修改后请重新验证，并告诉我验证结果。
```

## 7.2 你不知道错误在哪怎么办？

- 把浏览器控制台里的报错复制给 Codex。

- 把终端红色错误文本复制给 Codex。

- 描述“哪个按钮点了没反应”。

- 告诉它“我预期看到什么，实际上看到了什么”。

- 先让 Codex 诊断，不要一上来让它重写整个项目。

## 7.3 Hackathon 展示前的兜底

- 优先保证一条 Demo 主流程稳定可跑。

- 依赖 API 的项目准备一份稳定测试数据。

- 必要时准备备用 Demo 视频。

- 最后阶段停止大规模加功能，优先修会影响展示的问题。

[↩ 返回“快速定位”](#quick-start)　·　[↑ 返回目录](#toc)

<a id="prompt-templates"></a>
# 第 8 章　minicamp 常用 Prompt 模板

## 8.1 第一次接手项目

```text
先阅读当前项目，不要修改。告诉我项目结构、怎么运行、最重要的文件，以及你认为我接下来最应该先确认什么。
```

## 8.2 开发新功能

```text
我要增加【功能】。先分析现有项目和可能受影响的文件，给我一个最小实现计划；我确认后再修改。
```

## 8.3 修改 UI

```text
保持现有功能和数据逻辑不变，只调整【页面/组件】的视觉和交互。修改前告诉我准备改哪些文件。
```

## 8.4 Debug

```text
当前出现以下错误：【粘贴报错】。请先定位根因，再做最小修复；修复后重新运行/测试验证，不要通过删除功能绕过问题。
```

## 8.5 我看不懂代码

```text
我不熟悉【技术/文件】。请结合当前项目解释它为什么存在、输入是什么、输出是什么、修改它会影响哪里。
```

## 8.6 项目快结束了

```text
现在进入展示前收敛阶段。请检查主流程、明显 Bug、未完成但不影响展示的功能，并给出“必须修 / 可以砍 / 展示前确认”三栏清单。
```

[↩ 返回“快速定位”](#quick-start)　·　[↑ 返回目录](#toc)

<a id="preflight"></a>
# 第 9 章　赛前验收：做到这些就够了

□ 能访问 chatgpt.com，并能登录自己的账号。

□ VS Code 扩展 / ChatGPT 桌面端 / Codex CLI 至少一种入口可用。

□ Codex 能读取 minicamp-codex-demo。

□ Codex 能创建或修改 HTML / CSS / JavaScript 文件。

□ index.html 能在浏览器打开。

□ 番茄钟开始 / 暂停 / 重置基本正常。

□ 知道如何把报错、异常现象交给 Codex。

□ 知道不能把密码、Token、私钥粘给 AI。

## 9.1 30 秒速查表

> 1. 打开项目 / 工作区
> 2. 让 Codex 先读项目，不要急着改
> 3. 提需求：先分析 → 给计划 → 再修改
> 4. 改完自己运行 / 打开 Demo
> 5. 出错：复制报错 + 说清预期和实际结果
> 6. 大改前备份 / Git checkpoint
> 7. 展示前：少加功能，多保主流程

## 9.2 一句话路线总结

- **完全不会编程**：优先使用官方 ChatGPT 桌面端中的 Codex，先把“让 Codex 读项目、改文件、看到结果”这条链路跑通。

- **有编程基础，并且已经使用 VS Code**：直接安装 OpenAI 官方 Codex 扩展，通常是比赛现场最顺手的路线。

- **有编程基础，但没有 VS Code**：如果你习惯终端，可以直接使用 Codex CLI；如果不习惯终端，安装 VS Code + 官方 Codex 扩展会更直观。

- **Linux 零基础用户**：如果发行版在官方桌面端支持范围内，可以优先使用 ChatGPT Linux Preview；如果不在支持范围内，建议使用 VS Code + 官方 Codex 扩展。

- VS Code 扩展、ChatGPT 桌面端和 Codex CLI 是三条独立入口，不需要为了使用其中一种而先安装另外一种。

[↩ 返回“快速定位”](#quick-start)　·　[↑ 返回目录](#toc)

<a id="faq"></a>
# 常见问题 Q&A

**Q1：我没有 ChatGPT 账号。**

> 请先回到 [第 1.2 节：没有 ChatGPT 账号怎么办？](#account-signup) 完成账号注册。

**Q2：我只有免费账号。**

> 按文档当前核对结果，Free 也包含 Codex，但额度随方案而不同。可以先查看 [第 1.3 节：免费账号能不能用 Codex？](#free-plan)，再实际登录检查。

**Q3：我用 VS Code 插件，需要先装 Codex CLI 吗？**

> 不需要。VS Code 官方 Codex 扩展是独立入口；安装扩展、登录账号即可。

**Q4：VS Code 插件需要 Node.js 吗？**

> 仅为了使用官方 Codex 扩展，不需要。你自己的项目如果使用 Node.js，那是项目技术栈的需求，不是 Codex 扩展的前置条件。

**Q5：VS Code 里搜到很多 ChatGPT 插件。**

> 只装 OpenAI 官方 Codex 扩展，确认发布者为 OpenAI。

**Q6：装完插件看不到 Codex 图标。**

> Ctrl/Command + Shift + P，运行“Codex: Open Codex Sidebar”。

**Q7：Windows codex 命令不存在。**

> 如果你本来只打算用 VS Code 扩展，可以忽略 CLI；如果确实选择 CLI，再检查 Node/npm 和 npm 全局安装。

**Q8：macOS/Linux CLI 一定要 Node.js 吗？**

> 不需要。当前官方提供独立安装脚本 curl -fsSL https://chatgpt.com/codex/install.sh \| sh。

**Q9：Linux 能装官方 ChatGPT 桌面端吗？**

> 可以，但当前仍是 Preview，并且官方明确支持部分 Ubuntu / Debian / Fedora 桌面版本。其他发行版如果是零基础用户，建议优先使用 VS Code + 官方 Codex 扩展；熟悉终端的用户也可以直接使用 Codex CLI。

**Q10：Codex 改坏代码怎么办？**

> 停止继续改；用 VS Code 变更、Git checkpoint/commit 或 backup 文件夹回退，再让 Codex 基于真实错误做最小修复。

**Q11：我完全不会前端。**

> 可以让 Codex 限制技术栈、先规划、边做边解释；但你仍需自己运行和验证。

**Q12：能把密码、Cookie、Token 发给 Codex 吗？**

> 不要。登录只在官方登录/浏览器授权流程完成；不要把密码、Cookie、Token、私钥粘进聊天。

[↑ 返回目录](#toc)

---

<a id="appendix-a"></a>
# 附录 A　官方资料与版本说明

本教程在保留既有内容细节的基础上，于 2026-08-22 进一步整理署名、措辞、代码块标注与 Q&A 表述。OpenAI 产品更新较快；如果按钮名称、支持系统或安装方式变化，以官方页面最新说明为准。

**• ChatGPT 官网：**[https://chatgpt.com/](https://chatgpt.com/)

**• ChatGPT 官方下载：**[https://chatgpt.com/download/](https://chatgpt.com/download/)

**• Codex IDE 扩展官方文档：**[https://developers.openai.com/codex/ide](https://developers.openai.com/codex/ide)

**• Codex CLI 官方文档：**[https://developers.openai.com/codex/cli](https://developers.openai.com/codex/cli)

**• ChatGPT Linux 桌面端官方文档：**[https://learn.chatgpt.com/docs/linux/linux-app](https://learn.chatgpt.com/docs/linux/linux-app)

**• Codex 与 ChatGPT 方案说明：**[https://help.openai.com/en/articles/11369540-using-codex-with-your-chatgpt-plan/](https://help.openai.com/en/articles/11369540-using-codex-with-your-chatgpt-plan/)

**• VS Code 官网：**[https://code.visualstudio.com/](https://code.visualstudio.com/)

**• Node.js 官网（仅 Windows CLI npm 路线可能用到）：**[https://nodejs.org/](https://nodejs.org/)