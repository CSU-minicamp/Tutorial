# minicamp 2026 · AI Coding 环境与工具安装指南

本教程为MINICAMP团队成员创作，转载请注明出处 作者：**JiuYue-IT &#x20;**

**Windows / macOS / Linux · 按项目技术栈选择工具**

> **主要适用于 Windows。** 本指南的完整步骤以 Windows 11 和 PowerShell 为例；macOS 与 Linux 章节仅补充系统差异，并引用前文的相同流程。项目的 `README.md`、`.nvmrc`、`package.json`、`pyproject.toml` 或 `Dockerfile` 若规定版本，应始终以项目规定为准。
>
> **工具与环境均按项目需要选择，并非必须全部安装。** 只准备当前项目实际使用的语言运行时、依赖管理器、编辑器和包管理器；不要因为本指南列出了 Python、Node.js、uv、Poetry 或 pnpm 就同时安装或混用它们。
>
> **可以结合 AI 操作本指南。** 可向 AI 提供你的操作系统、项目 README、当前目录与完整报错，请它解释下一步或检查命令；执行前仍应阅读命令和 `git diff`，并且绝不发送 API Key、密码、私钥、`.env` 或其他敏感信息。

## 目录

- [第 1 章　安装前检查](#1-安装前检查)
  - [1.1 打开 PowerShell](#11-打开-powershell)
    - [常用 PowerShell 命令](#常用-powershell-命令)
  - [1.2 所有章节通用：先检查，再安装](#12-所有章节通用先检查再安装)
  - [1.3 项目文件夹与路径](#13-项目文件夹与路径所有-cd-命令的使用规则)
- [第 2 章　终端](#2-终端)
  - [2.1 Windows Terminal（推荐）](#21-windows-terminal推荐)
    - [Windows Terminal 常用命令](#windows-terminal-常用命令)
- [第 3 章　Git 与 GitHub](#3-git-与-github)
  - [3.1 安装 Git](#31-安装-git)
  - [3.2 配置身份](#32-配置身份)
  - [3.3 创建 GitHub SSH 密钥](#33-创建-github-ssh-密钥)
  - [日常 Git 命令](#日常-git-命令)
- [第 4 章　代码编辑器与 AI 编程工具](#4-代码编辑器与-ai-编程工具)
  - [4.1 VS Code](#41-vs-code)
    - [VS Code 常用命令](#vs-code-常用命令)
  - [4.2 推荐 AI 工具与简易流程](#42-推荐-ai-工具与简易流程)
- [第 5 章　Python](#5-python)
  - [5.1 安装 Python](#51-安装-python)
    - [Python 常用命令](#python-常用命令)
  - [5.2 选择 Python 环境与依赖工作流](#52-为每个项目选择-python-环境与依赖工作流)
- [第 6 章　Node.js、npm 与 pnpm](#6-nodejsnpm-与-pnpm)
  - [6.1 安装 Node.js LTS](#61-安装-nodejs-lts)
  - [6.2 启用 pnpm（按项目需要）](#62-启用-pnpm按项目需要)
    - [Node.js 与 pnpm 常用命令](#nodejs-与-pnpm-常用命令)
- [第 7 章　代码质量与基础验证](#7-代码质量与基础验证)
- [第 8 章　Windows 一次性检查清单](#8-windows-一次性检查清单)
- [第 9 章　Windows 推荐安装顺序](#9-windows-推荐安装顺序)
- [第 10 章　macOS 简明指南](#10-macos-简明指南)
  - [10.1 需要的工具](#101-需要的工具)
  - [10.2 首次设置](#102-首次设置)
  - [10.3 与 Windows 不同的命令](#103-与-windows-不同的命令)
- [第 11 章　Linux 简明指南](#11-linux-简明指南)
  - [11.1 需要的工具](#111-需要的工具)
  - [11.2 首次设置](#112-首次设置)
  - [11.3 与 Windows 不同的命令](#113-与-windows-不同的命令)
- [附录　官方参考](#官方参考)

---

# 1. 安装前检查

## 1.1 打开 PowerShell

**作用：** PowerShell 是 Windows 的命令行环境，用于执行本指南中的检查、安装、Git、Python 和 Node 命令；`winget` 是 Windows 的软件包安装器。

**是否需要：** PowerShell 已随 Windows 提供，必需使用其中一种终端执行命令。`winget` 强烈推荐，可统一安装软件；也可改用每个工具的官网安装包。

按 `Win` 键，搜索 **PowerShell**，打开后执行：

```powershell
$PSVersionTable.PSVersion
winget --version
```

若 `winget` 不存在，先在 Microsoft Store 更新/安装 **App Installer**，再重新打开终端。本文用 `winget` 安装多数软件；也可改为各节提供的官网安装包。

重新打开后再次执行 `winget --version`。若仍不可用或设备禁止 Microsoft Store，请记录限制并改用各工具官网安装包；不要在后文重复尝试同一条 `winget` 命令。

> 安装软件后请关闭并重新打开 PowerShell，使 PATH 更新生效。

### 常用 PowerShell 命令

```powershell
Get-Location              # 显示当前所在文件夹
Get-ChildItem -Force      # 列出当前文件夹内容（含 .git 等隐藏项）
Set-Location "D:\项目路径" # 进入指定项目文件夹；cd 是它的简写
Clear-Host                # 清空当前终端显示
```

## 1.2 所有章节通用：先检查，再安装

本指南不假设电脑是全新的。每一项均按以下规则操作：

1. 先执行该项的“安装前检查”。若命令能显示版本且符合项目要求，**跳过安装步骤**。
2. 若命令报“找不到”，才执行该项的安装命令。
3. 若显示版本但与项目要求不符，先查看命令位置；不要直接重装或卸载。优先用项目规定的版本管理方式处理。
4. 若 `where.exe` 返回多个路径，表示可能装有多个版本；保留现状并确认实际调用版本后再调整。

通用的版本与路径检查格式如下：

```powershell
<命令> --version
where.exe <命令>
```

> `where.exe` 没有结果不一定是故障：Windows Store 的 Python 别名等场景不会按常规 PATH 显示。以实际的版本命令结果和项目要求为准。

每次安装或切换版本后，都应关闭并重新打开终端，再重复该工具的“安装前检查”。只有版本与实际调用路径均符合预期，才继续下一节。

## 1.3 项目文件夹与路径：所有 `cd` 命令的使用规则

文中的 `C:\path\to\project`、`REPOSITORY`、`OWNER/REPOSITORY`、`你的项目名` 都是**占位示例**，不能原样复制执行。请将其替换为你电脑上真实的项目文件夹或仓库名称。后文所说的“项目根目录”，是指包含项目的 `README.md`、`.git`、`package.json`、`pyproject.toml` 等文件之一的最外层文件夹。

不要在 `C:\Windows\System32`、`C:\Program Files` 或软件安装目录中创建项目、`.venv`、`.env` 或代码文件；请使用自己的用户目录、专门的代码目录或团队规定的位置。

### 创建新的项目文件夹

以下示例会在当前 Windows 用户目录下新建 `source\my-project`。`my-project` 需要替换为你的项目名：

```powershell
New-Item -ItemType Directory -Path "$env:USERPROFILE\source\my-project" -Force
Set-Location "$env:USERPROFILE\source\my-project"
Get-Location
```

例如，你的 LLM 学习项目可命名为 `llm-learning`，对应路径通常为 `C:\Users\你的用户名\source\llm-learning`。

### 打开已有项目文件夹

方式一：在 PowerShell 中将引号内的路径改成已有项目的真实路径：

```powershell
Test-Path -LiteralPath "D:\实际位置\项目文件夹"
Set-Location -LiteralPath "D:\实际位置\项目文件夹"
Get-Location
```

仅当第一条命令返回 `True` 时才执行 `Set-Location`；若返回 `False`，先在文件资源管理器确认路径和盘符，不要猜测或创建同名目录。

方式二：在文件资源管理器中进入项目文件夹，点击地址栏，输入 `powershell` 并按 Enter，即可在该文件夹打开 PowerShell。

进入正确目录后，再执行项目相关命令。例如用 VS Code 打开当前项目：

```powershell
code .
```

> 判断是否进入正确目录：执行 `Get-ChildItem -Force`。已有 Git 项目通常会看到 `.git`；Python/Node 项目通常会看到 README、依赖描述或锁定文件。新建的空项目则暂时没有这些文件。

# 2. 终端

## 2.1 Windows Terminal（推荐）

**作用：** 提供带标签页、分屏、主题和多终端配置的命令行窗口，可统一使用 PowerShell 和命令提示符。

**是否需要：** 推荐安装，但不是必需。只要现有 PowerShell 用得顺手，可以跳过；若要频繁运行 Git、Python 或 Node 命令，建议保留。

**安装前检查：**

```powershell
wt --version
Get-Command wt -ErrorAction SilentlyContinue
```

若能显示版本，跳过安装；否则执行：

```powershell
winget install --id Microsoft.WindowsTerminal -e
```

安装完成后关闭并重新打开终端，再执行 `wt --version`。随后打开 Windows Terminal，在设置中将默认配置文件设为 **PowerShell**。

验证：

```powershell
wt --version
```

### Windows Terminal 常用命令

```powershell
wt              # 打开新的 Windows Terminal 窗口
wt -d .         # 在当前文件夹打开新的 Windows Terminal 窗口
```

# 3. Git 与 GitHub

## 3.1 安装 Git

**作用：** 记录代码变更历史、创建分支、合并协作成果，并与 GitHub、GitLab、Gitee 等代码仓库同步。

**是否需要：** 几乎所有 AI Coding 项目都需要，应安装。即使 AI 能生成代码，仍需用 Git 查看改动、回退错误和提交成果。

**安装前检查：**

```powershell
git --version
where.exe git
```

若版本符合项目要求，跳过安装；否则在确认路径与版本策略后再执行：

```powershell
winget install --id Git.Git -e --source winget
```

图形安装时保留默认选项即可；确保选择将 Git 加入命令行 PATH 的选项。

安装完成后关闭并重新打开终端，再验证：

```powershell
git --version
```

## 3.2 配置身份

**作用：** 将你的姓名和邮箱写入后续 Git 提交，便于团队追踪提交来源。

**是否需要：** 需要提交代码时必须配置；若只是浏览或下载代码可暂缓。

**安装前检查：**

```powershell
git config --global --get user.name
git config --global --get user.email
```

若两项均正确，跳过配置。只有缺失或需要更正时，才执行：

将下列姓名、邮箱替换为自己的信息。邮箱应与代码托管平台账户匹配：

```powershell
git config --global user.name "你的名字"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global --list
```

最后逐项确认实际写入的值；若显示不正确，只重运行对应的一条 `git config --global` 命令，不需要重装 Git：

```powershell
git config --global --get user.name
git config --global --get user.email
git config --global --get init.defaultBranch
```

## 3.3 创建 GitHub SSH 密钥

**作用：** 让电脑以加密密钥向 GitHub 证明身份，免去每次 `git push` 输入账号或令牌。

**是否需要：** 使用 GitHub 的私有仓库、需要推送代码时推荐配置；只下载公开仓库、或团队统一使用 HTTPS/企业凭据时可跳过。

黑客松团队建议在开发开始时就确定一个共享仓库：由一名成员创建仓库、邀请队友协作并让每个人各自用自己的 SSH/账号推送。仓库可保持私有；是否公开由团队自行决定。不要共用同一 GitHub 账号或互相发送私钥。

请先按下面四步完成 SSH 认证，再创建或克隆共享仓库；这样可避免在 `git clone` 或第一次推送时才发现权限问题。

**第 1 步：检查已有密钥与认证。**

```powershell
Test-Path "$env:USERPROFILE\.ssh\id_ed25519.pub"
ssh -T git@github.com
```

若第二条命令显示认证成功，直接跳到“第 5 步：黑客松共享仓库”；这表示 SSH 可能正在使用其他已配置的密钥。若第一条返回 `True` 但认证失败，不要覆盖私钥；执行下列命令复制现有公钥，并在 GitHub 检查它是否添加到了当前使用的账号：

```powershell
Get-Content "$env:USERPROFILE\.ssh\id_ed25519.pub" | Set-Clipboard
```

**第 2 步：仅在没有默认公钥且认证失败时创建密钥。**

```powershell
ssh-keygen -t ed25519 -C "you@example.com"
```

将邮箱替换为自己的 GitHub 邮箱。一路按 Enter 使用默认路径；是否设置密码短语按个人安全要求决定。命令完成后确认公钥确实已生成：

```powershell
Test-Path "$env:USERPROFILE\.ssh\id_ed25519.pub"
```

**第 3 步：将公钥添加到 GitHub。**

```powershell
Get-Content "$env:USERPROFILE\.ssh\id_ed25519.pub" | Set-Clipboard
```

在 GitHub 进入 **Settings → SSH and GPG keys → New SSH key**，粘贴并保存。只复制 `.pub` 公钥内容，绝不发送或上传没有 `.pub` 后缀的私钥文件。

**第 4 步：验证认证。**

```powershell
ssh -T git@github.com
```

首次连接时核对主机名为 `github.com` 后输入 `yes`。成功后会显示认证成功的信息；若仍失败，先确认第 3 步保存的是当前电脑的公钥和正确的 GitHub 账号，再重试。

### 第 5 步：黑客松共享仓库

以下以 GitHub 为例。团队应在开始写核心功能前完成一次全员拉取与推送验证；若使用 GitLab/Gitee，步骤与术语相同。

1. **确定负责人和仓库名。** 选一位成员作为仓库 Owner，另选一位成员保留完整本地副本并熟悉部署方式。仓库名用简短英文小写和连字符，例如 `campus-helper`；不要把 API Key、手机号等敏感信息写入仓库名。
2. **创建仓库。** Owner 在 GitHub 右上角点击 **+ → New repository**，填写仓库名。黑客松开发期建议先选 **Private**，在提交时由团队决定是否公开。勾选 **Add a README file**，并按技术栈选择 `.gitignore` 模板（Python、Node 等），然后点击 **Create repository**。
3. **邀请所有队友。** 在仓库页进入 **Settings → Collaborators**（或 **Collaborators & teams**）→ **Add people**，按 GitHub 用户名逐个邀请。队友必须在 GitHub 通知或邮箱中接受邀请；未接受前无法推送私有仓库。
4. **每位队友克隆仓库。** 每个人在仓库页面点击 **Code → SSH**，复制地址；在自己电脑的代码父目录执行（将地址替换为复制结果）：

   ```powershell
   Set-Location -LiteralPath "D:\实际位置\代码父目录"
   git clone git@github.com:OWNER/REPOSITORY.git
   Set-Location .\REPOSITORY
   git remote -v
   git status
   ```

   `git remote -v` 应显示名为 `origin` 的 GitHub 地址，`git status` 应显示工作区干净。若 clone 时报权限错误，先检查本章的 SSH 认证；若显示仓库不存在，检查邀请是否已接受及 SSH 地址是否正确。
5. **每位队友验证能推送。** 不要多人直接改 `main` 做测试。每人用自己的 GitHub 用户名创建一个一次性分支和唯一文件：

   ```powershell
   git switch -c setup/你的GitHub用户名
   New-Item -ItemType File -Path "team-check-你的GitHub用户名.txt"
   git add "team-check-你的GitHub用户名.txt"
   git commit -m "chore: verify team access"
   git push -u origin HEAD
   ```

   浏览器刷新仓库后应看到该分支。Owner 可为每个分支创建并合并 Pull Request，或在全员验证后删除这些测试分支/文件。这样可在正式开发前发现账号权限或 SSH 问题。
6. **约定两天内的最小协作规则。**
   - `main` 始终保持可运行、可演示；指定一位成员负责合并和部署。
   - 每项功能在独立分支开发，例如 `feat/login`、`fix/api-timeout`；开始新任务时先执行 `git switch main`、`git pull --ff-only origin main`，再执行 `git switch -c feat/功能名` 创建新分支；完成后提交并合并。
   - 提交应小而清楚，例如 `feat: add event list`、`fix: handle empty query`；不要把多个无关改动堆成一次提交。
   - 任何 `.env`、密钥、个人配置文件均不得提交；需要共享配置时只提交 `.env.example`。
   - 发生冲突、构建失败或准备部署时优先通知团队；不要用强制推送覆盖别人的分支，除非分支拥有者明确同意。

### 日常 Git 命令

在项目根目录执行：

```powershell
git status                         # 查看修改、当前分支和待提交文件
git diff                           # 查看尚未暂存的代码改动
git add <文件名>                    # 暂存指定文件；不要无检查地使用 git add .
git commit -m "feat: 简要说明改动"  # 将暂存改动创建为一次本地提交
git pull --ff-only origin main     # 更新本地 main，避免自动产生合并提交
git push                            # 推送当前分支已提交的改动
git log --oneline -5               # 查看最近 5 次提交
```

提交前先运行 `git status` 与 `git diff --cached`，确认不会提交 `.env`、密钥或无关文件。

# 4. 代码编辑器与 AI 编程工具

## 4.1 VS Code

**作用：** 编写、搜索、调试代码，并通过扩展支持 Python、Node.js、Git 及 AI 编程助手。

**是否需要：** 推荐安装，是最通用的编辑器选择；若已使用 Cursor、JetBrains 等其他编辑器且项目支持，可跳过。

黑客松中团队成员不必使用同一编辑器；关键是每个人都能打开团队仓库、运行项目，并能看到 Git 变更。建议在活动前用任意一个小项目测试一次“打开文件夹 → 修改 → 运行 → 提交/推送”的完整流程。

**安装前检查：**

```powershell
code --version
where.exe code
```

若版本能正常显示，跳过安装。若 VS Code 已安装但 `code` 找不到，先完全关闭 VS Code 与终端并重开；仍无效时，在 VS Code 中按 `Ctrl+Shift+P`，运行 **Shell Command: Install 'code' command in PATH**。只有未安装时，才执行：

```powershell
winget install --id Microsoft.VisualStudioCode -e
```

重新打开终端，验证：

```powershell
code --version
```

在 VS Code 中按 `Ctrl+Shift+X` 打开扩展市场，按项目语言安装：

- **Python**（Microsoft）与 **Pylance**：Python 项目。
- **ESLint**、**Prettier - Code formatter**：JavaScript/TypeScript 项目。
- **GitLens**（可选）：增强 Git 历史与代码追溯。

扩展安装完成后，先关闭并重新打开 VS Code；打开项目时若出现工作区信任提示，只对来源可信的仓库选择 **Trust**。Python 项目创建 `.venv` 后，再按 `Ctrl+Shift+P`，运行 **Python: Select Interpreter**，选择该项目的 `.venv\Scripts\python.exe`；否则编辑器的运行与补全可能仍使用全局 Python。

建议在 VS Code 打开项目根目录，而不是单个文件：

```powershell
# 先按“1.3 项目文件夹与路径”进入真实的项目根目录
code .
```

### VS Code 常用命令

```powershell
code .                 # 用 VS Code 打开当前项目文件夹
code -g "README.md:1"  # 打开文件并跳转到指定行
code --reuse-window .  # 在当前 VS Code 窗口打开项目
```

## 4.2 推荐 AI 工具与简易流程

下列工具都能协助理解、修改和验证代码，但没有“所有项目都最适合”的唯一选择。先选一个与团队账号、预算、代码数据政策和工作习惯相符的工具即可；不要同时让多个 AI 助手对同一批文件自动改动。

| 工具 | 适合的使用方式 | 开始前确认 |
| --- | --- | --- |
| [Codex](https://developers.openai.com/) | 希望让 AI 以任务为单位理解仓库、规划改动、编辑文件并运行验证的开发者。 | 账号可用范围、工作区权限、命令与写入操作的审批方式。 |
| [Claude Code](https://code.claude.com/docs/en/overview) | 偏好在终端或 IDE 中让代理跨文件处理功能、调试和测试任务的开发者。 | 账号/订阅、终端权限，以及是否允许它运行项目命令。 |
| [Cursor](https://docs.cursor.com/chat/overview) | 希望使用集成 AI 的编辑器，在代码库上下文中聊天、编辑和审查差异的开发者。 | 是否迁移现有编辑器设置、模型/隐私选项和团队许可。 |
| [VS Code + AI 插件](https://code.visualstudio.com/docs/chat/chat-overview) | 已将 VS Code 作为团队标准，想保留现有扩展、调试和 Git 工作流的开发者。 | 只安装一个团队认可的 AI 助手插件，并确认其登录、数据与权限设置。 |

**简易使用流程：**

1. **先准备项目。** 进入项目根目录，阅读 README，执行 `git status`；重要工作先创建分支，确保没有不清楚的本地修改。
2. **给出完整但非敏感的上下文。** 告诉 AI 目标、相关文件、技术栈、约束条件和验收标准；可粘贴已脱敏的错误信息，但绝不提供 `.env`、API Key、密码、令牌或私钥。
3. **先要方案，再要改动。** 先让 AI 说明将查看哪些文件、准备如何修改、要运行哪些检查；确认方案后，再授权它修改小而独立的一项功能。
4. **限制执行范围。** 仅允许项目所需的安装、测试、构建或格式化命令；遇到删除、覆盖、上传、部署或访问外部服务的操作时，先停下来人工确认。
5. **人工审查结果。** 执行 `git diff`，逐项检查变更；再按第 7 节运行 README 规定的检查、测试、构建和启动流程。AI 的“已完成”不等于项目已经正确。
6. **验证后再提交。** 在浏览器/客户端走一遍核心功能，确认无误后再提交。提交前再次运行 `git status`，确保没有将 `.env`、密钥或无关文件纳入提交。

一个适合开始时使用的提示示例：`先阅读 README 和相关文件，不要修改。请给出实现“<目标>”的最小方案、预计会改动的文件、风险，以及应运行的验证命令。` 确认方案后，再让工具执行单个小步骤。

# 5. Python

## 5.1 安装 Python

**作用：** 运行 Python 项目、自动化脚本、数据处理、后端服务及多数 AI/机器学习工具链。

**是否需要：** 项目含 `requirements.txt`、`pyproject.toml`、`.py` 文件，或你要做 AI/数据/后端 Python 开发时需要；纯 Node.js、前端或其他语言项目可跳过。

黑客松中只有选择 Python 技术栈的团队才需要本节；不要因为活动涉及 AI Coding 就给所有电脑安装 Python。若项目同时使用前端与 Python 后端，再按第 6 节准备 Node.js。

**安装前检查：**

```powershell
python --version
py --version
python -m pip --version
where.exe python
where.exe py
```

若 `python` 或 `py` 显示的版本符合项目要求，跳过安装。若存在多个版本，先查看项目的 `pyproject.toml`、`.python-version`、`runtime.txt` 或 README；可用 `py -0p` 查看 Python Launcher 识别到的解释器。创建虚拟环境时必须明确使用其中一个版本：用 `python -m venv` 保持与 `python --version` 一致，或用 `py -3.12 -m venv` 这类形式精确指定版本；不要直接使用未指定版本的 `py -m venv`。只有未安装或确定需要新增项目所需版本时，才继续：

优先安装项目指定的 3.x 版本；没有规定时选择当前稳定版。可从 [Python 官网下载页](https://www.python.org/downloads/windows/) 获取官方安装器。安装器首屏勾选 **Add python.exe to PATH**，然后选择 **Install Now**。

安装后验证：

```powershell
python --version
py --version
python -m pip --version
```

如系统存在多个 Python，优先使用 `py -3.x` 显式指定版本，例如 `py -3.12 --version`。

### Python 常用命令

```powershell
python script.py          # 运行当前目录的 Python 脚本
python -m pip list        # 查看当前 Python 环境已安装的软件包
python -m pip show 包名    # 查看某个软件包的版本与安装位置
deactivate                # 退出已激活的 (.venv)；未激活时无需执行
```

## 5.2 为每个项目选择 Python 环境与依赖工作流

**核心结论：不要任意搭配。** 每个项目应选择一种依赖管理工作流；`pip`、uv 与 Poetry 是执行安装/同步的工具，`requirements.txt`、`pyproject.toml`、`uv.lock`、`poetry.lock` 是项目文件，`.venv` 只是隔离依赖的目录。它们的角色不同，不能因为文件同时存在就把所有命令都运行一遍。

文件之间的关系如下：`pyproject.toml` 用于声明项目元数据、Python 版本和依赖，**本身不指定**必须使用 pip、uv 或 Poetry；`requirements.txt` 是给安装工具读取的包清单，可能是手写声明，也可能是从其他工具导出的精确版本；`uv.lock` 与 `poetry.lock` 则是各自工具解析出的完整精确版本快照，供团队复现同一套依赖。换言之，`pyproject.toml` 是“项目要什么”，锁定文件是“本次确定用哪些精确版本”，而 pip/uv/Poetry 是“谁来安装它们”。

| 工作流 | 应看到的核心文件 | 只使用的工具与命令 | 不要混用 |
| --- | --- | --- | --- |
| pip + `requirements.txt` | `requirements.txt` | `python -m pip install -r requirements.txt` | 不运行 `uv sync` 或 `poetry install`。 |
| pip + 标准 `pyproject.toml` | `pyproject.toml`，且没有 `uv.lock`、`poetry.lock`、`[tool.uv]` 或 `[tool.poetry]` | `python -m pip install -e .` | 不自行生成或采用 uv/Poetry 锁定文件。 |
| uv | `pyproject.toml` + `uv.lock` | `uv sync`、`uv run ...` | 不用 pip 或 Poetry 安装同一项目依赖。 |
| Poetry | `pyproject.toml` + `poetry.lock`，或含 `[tool.poetry]` | `poetry install`、`poetry run ...` | 不用 pip 或 uv 安装同一项目依赖。 |

几点必须记住：

- `requirements.txt` 与 `pyproject.toml` **可以同时存在**，但不代表两条安装命令都要运行。它常见于“主项目用 `pyproject.toml`，另提供 `requirements.txt` 给部署/旧工具”的场景；以 README、CI 和团队约定指定的那一个为准。
- `uv.lock` 只由 uv 使用；`poetry.lock` 只由 Poetry 使用。两者不能搭配，也不应同时作为同一项目的依赖真相来源。
- `.venv` 可以由 pip、uv 或 Poetry 创建，因此它本身**不能**用来判断该执行哪个工具；要先看锁定文件和 README。选定 uv 或 Poetry 后，不要手动在同一目录用 `python -m venv .venv` 覆盖它。
- `pip` 是 Python 自带的安装工具，不是项目文件。它只用于本节的两个 pip 工作流；使用 uv 或 Poetry 的项目不需要再用 pip 安装项目依赖。

**第 1 步：进入项目根目录。** 路径必须替换为你的真实项目路径：

```powershell
Set-Location -LiteralPath "D:\LLM_projects\rag-learning"
Get-Location
```

若项目位置不同，请按 [1.3 项目文件夹与路径](#13-项目文件夹与路径所有-cd-命令的使用规则) 的方法进入。确认 `Get-Location` 显示的是项目文件夹后，再继续下一步；不要在 `C:\Windows\System32` 等系统目录执行后续命令。

**第 2 步：只做一次文件识别。** 先阅读 README，然后执行下列命令；它只列出实际存在的相关文件，不会给出一串 `True`/`False`：

```powershell
Get-ChildItem -Force | Where-Object { $_.Name -in @('requirements.txt', 'pyproject.toml', 'uv.lock', 'poetry.lock') } | Select-Object -ExpandProperty Name
```

将输出与上表比对后，只进入一个对应流程；不要继续执行其他流程的检查或命令。若同时出现 `uv.lock` 和 `poetry.lock`，或 README 与文件组合相互矛盾，停止操作并询问项目维护者。

### 流程 A：pip + `requirements.txt`

**适用条件：** README 明确要求 pip，且 `requirements.txt` 是项目指定的依赖清单。即使同时有 `pyproject.toml`，也只有 README/CI 明确将 `requirements.txt` 作为本地开发入口时才使用本流程。

先准备 pip 的 `.venv`。只检查这一项：若下面命令返回 `True`，执行第一个代码块；返回 `False`，执行第二个代码块。

```powershell
Test-Path .venv
```

已有 `.venv`：

```powershell
.\.venv\Scripts\Activate.ps1
python --version
```

没有 `.venv`：

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python --version
```

命令提示符出现 `(.venv)` 后，安装并验证依赖：

```powershell
python -m pip install -r requirements.txt
python -m pip check
```

### 流程 B：pip + 标准 `pyproject.toml`

**适用条件：** README 未指定 uv、Poetry、Conda 或 Docker；`pyproject.toml` 使用标准 `[project]` / `[build-system]`，并且项目没有 `uv.lock`、`poetry.lock`、`[tool.uv]` 或 `[tool.poetry]`。

按流程 A 的“准备 pip 的 `.venv`”步骤激活或创建环境，然后只执行：

```powershell
python -m pip install -e .
python -m pip check
```

`-e` 表示可编辑安装：修改项目源代码后无需重新安装。若 `pyproject.toml` 中有 `[dependency-groups]`，仅在 README 要求相应开发组时再安装，例如：

```powershell
python -m pip install --group dev
```

该选项需要 pip 25.1+。若当前 pip 版本过低，先在已激活的 `.venv` 中执行 `python -m pip install --upgrade pip`，再执行指定的组安装命令。

### 流程 C：新项目或无法判定

没有任何依赖文件时，不运行 `pip install`、`uv sync` 或 `poetry install`。先查看 README、团队文档和仓库分支是否遗漏说明；若这是一个新建个人项目，本指南推荐转到 5.3，用 `uv init` 建立 `pyproject.toml` + `uv.lock` 的 uv 工作流。

如果 PowerShell 阻止 pip 工作流激活 `.venv`，仅为当前终端执行：

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

然后重新运行对应的 `Activate.ps1`。不要为了此问题把系统范围的执行策略改成不受限制。

## 5.3 uv（推荐给新项目）

**作用：** 快速创建 Python 环境、安装依赖和锁定版本，可替代部分 `pip + venv` 工作流。

**是否需要：** 新建 Python 项目或项目含 `uv.lock` 时推荐；现有项目使用 `requirements.txt`、Poetry 或 Conda 时不必安装。

**安装前检查：**

```powershell
uv --version
where.exe uv
```

若已安装，跳过安装。现有项目若含 `uv.lock` 或 `[tool.uv]` 配置，再使用 uv；若项目使用 `requirements.txt`、Poetry 或 Conda，不要仅因本指南而迁移。`uv` 可快速管理 Python 版本和依赖；未安装且新项目需要时执行：

```powershell
winget install --id astral-sh.uv -e
uv --version
```

现有 uv 项目应在含 `uv.lock` 的项目根目录依次执行：

```powershell
uv sync
uv run python --version
```

`uv sync` 完成后由 uv 创建或更新项目的 `.venv`；日常执行命令优先使用 `uv run <命令>`，例如 README 指定的测试命令。不要在同一项目中再手动执行 `python -m venv .venv` 或 `pip install`。

新项目示例：

```powershell
mkdir demo-python
cd demo-python
uv init
uv add requests
uv sync
uv run python -c "import requests; print(requests.__version__)"
```

## 5.4 Poetry（仅当项目使用 Poetry 时）

**作用：** Poetry 是另一种 Python 项目与依赖管理工具；它读取 `pyproject.toml`、维护 `poetry.lock`，并安装可复现的项目环境。

**是否需要：** 仅当项目有 `poetry.lock`、`[tool.poetry]`，或 README 明确要求 Poetry 时安装。不要因为本指南包含本节而给 uv/pip 项目安装 Poetry。

**安装前检查：**

```powershell
poetry --version
where.exe poetry
```

若 Poetry 已存在且版本符合项目要求，跳过安装。若项目确实需要而尚未安装，按以下两个位置区分操作：

1. **安装 Poetry 工具的位置：** 打开一个普通的新 PowerShell 窗口，且不要激活任何项目的 `(.venv)`。安装命令可在任意非项目目录运行；它会将 Poetry 作为当前 Windows 用户的独立工具安装到 `%APPDATA%\pypoetry`，**不是**安装到项目的 `.venv`。
2. **运行 `poetry install` 的位置：** 安装完成后，进入含有 `pyproject.toml` 与（通常还有）`poetry.lock` 的**项目根目录**，再运行。Poetry 会按项目配置创建或使用它管理的虚拟环境。

在普通、未激活 `.venv` 的 PowerShell 中运行 Poetry 官方 Windows 安装器：

```powershell
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | py -
```

安装完成后关闭并重新打开 PowerShell，再验证：

```powershell
poetry --version
```

若提示找不到 `poetry`，请检查 `%APPDATA%\Python\Scripts` 是否在 PATH 中；也可暂时使用完整路径 `%APPDATA%\pypoetry\venv\Scripts\poetry`。然后进入真实的项目根目录并安装项目依赖：

```powershell
Set-Location -LiteralPath "D:\实际位置\项目文件夹"
Get-Location
poetry install
poetry run python --version
```

`poetry install` 完成后，优先用 Poetry 在项目环境中执行 README 指定的命令，例如 `poetry run pytest`；除非 README 明确要求，否则不需要手动激活 Poetry 管理的环境。若安装失败，先运行 `poetry check` 查看项目配置，而不是删除锁定文件或改用 pip。

# 6. Node.js、npm 与 pnpm

## 6.1 安装 Node.js LTS

**作用：** 运行 JavaScript/TypeScript 的前端、后端、构建工具（如 Vite、Next.js）和许多开发脚本；npm 随 Node.js 一起提供。

**是否需要：** 项目含 `package.json`、使用 React/Vue/Next.js/NestJS 等生态时需要；纯 Python 或不含 JavaScript 工具链的项目可跳过。

黑客松中选择网站前端、Node.js 后端、小游戏工具链或 JavaScript/TypeScript 框架的团队通常需要本节；纯 Python、原生移动端或硬件项目可跳过。

**安装前检查：**

```powershell
node --version
npm --version
where.exe node
where.exe npm
```

若 Node.js 版本符合项目 `package.json` 的 `engines.node` 或 `.nvmrc` 要求，跳过安装。若路径中出现 `nvm`、`fnm`、Volta 等版本管理器，使用该工具切换版本，不要用 winget 覆盖安装。只有未安装或确定需要全局 LTS 版本时，才执行：

```powershell
winget install --id OpenJS.NodeJS.LTS -e
```

安装完成后关闭并重新打开终端，再验证：

```powershell
node --version
npm --version
```

不要同时安装多个全局 Node 版本管理器。若不同项目要求不同 Node 版本，再考虑安装 `fnm` 或 `nvm-windows`，并以仓库 `.nvmrc` 或 `package.json` 的 `engines` 字段为准。

## 6.2 启用 pnpm（按项目需要）

**作用：** JavaScript/TypeScript 的依赖安装工具，通常比 npm 更节省磁盘，并严格复用锁定版本。

**是否需要：** 仅当项目含 `pnpm-lock.yaml` 或 README 明确要求 pnpm 时需要；项目使用 `package-lock.json` 时使用 npm，使用 `yarn.lock` 时使用 Yarn。

**安装前检查：**

```powershell
pnpm --version
where.exe pnpm
corepack --version
```

若 `pnpm --version` 能显示版本且与项目 `packageManager` 字段相符，跳过启用步骤。只有项目含 `pnpm-lock.yaml` 或明确要求 pnpm、且未安装时，才继续。若项目使用 npm 或 Yarn，本节不需要执行。

先进入含 `package.json` 的项目根目录，检查锁定文件和项目声明；不要只凭个人习惯选择包管理器：

```powershell
Test-Path package.json
Test-Path package-lock.json
Test-Path pnpm-lock.yaml
Test-Path yarn.lock
Get-Content .\package.json
```

第一条命令必须返回 `True`。重点查看 `packageManager` 字段和 README；若它与锁定文件矛盾，先向团队确认，不要运行安装命令。

若当前 Node.js 发行版提供 Corepack，可用它管理 pnpm：

```powershell
corepack enable
pnpm --version
```

Corepack 会读取项目 `package.json` 中的 `packageManager` 字段并按其声明管理版本。若 `pnpm --version` 仍找不到命令，先重新打开终端；若当前 Node.js 发行版未提供 `corepack`，按项目 README 或 pnpm 官方安装方式安装与团队一致的版本。不要在未确认项目版本时全局安装 `pnpm@latest`。

在项目中，根据锁定文件选择唯一的包管理器：

| 看到的文件 | 使用的命令 |
| --- | --- |
| `package-lock.json` | `npm ci` |
| `pnpm-lock.yaml` | `pnpm install --frozen-lockfile` |
| `yarn.lock` | `yarn install --immutable`（Yarn Berry）或按 README 执行 |
| 没有锁定文件 | 先阅读 README 和团队说明；首次安装会创建锁定文件，需按团队约定执行，不能套用 `npm ci`。 |

只执行表中匹配的一条安装命令。不要混用 `npm install`、`pnpm install` 与 `yarn install`，否则会改变锁定文件或造成依赖不一致。安装完成后再执行对应的 `<包管理器> run`，查看项目实际定义了哪些脚本。

### Node.js 与 pnpm 常用命令

均在含 `package.json` 的项目根目录执行：

```powershell
npm run                   # 列出项目定义的脚本
npm run dev               # 启动开发服务器（仅当项目定义 dev 脚本时）
npm run build             # 构建项目（仅当项目定义 build 脚本时）
pnpm run                  # pnpm 项目中列出脚本
pnpm run dev              # pnpm 项目中启动开发服务器（仅当项目定义 dev 脚本时）
```

# 7. 代码质量与基础验证

按以下顺序在每次首次拉取、合并较大改动或准备演示前验证项目。README、团队文档和 CI 配置优先于本节；不要把所有示例命令连续复制执行。

**第 1 步：取得或确认本地项目副本。** 已有本地副本时，先进入项目根目录并确认状态：

```powershell
git status
git remote -v
```

若尚未克隆，先完成 3.3 的 SSH 认证，再在代码父目录执行：

```powershell
Set-Location -LiteralPath "D:\实际位置\代码父目录"
git clone git@github.com:OWNER/REPOSITORY.git
Set-Location .\REPOSITORY
git status
```

将 `OWNER/REPOSITORY` 和 `REPOSITORY` 替换为真实名称。只有工作区干净、且团队确认当前分支可更新时，才执行 `git pull --ff-only origin main`；默认分支不是 `main` 时按 `git remote show origin` 或团队说明替换分支名。

**第 2 步：识别项目约定。**

```powershell
Test-Path README.md
Test-Path package.json
Test-Path pyproject.toml
Test-Path requirements.txt
Get-ChildItem -Force
```

阅读 README、`package.json` 或 `pyproject.toml`，确认所需的运行时版本、锁定文件、包管理器、环境变量、数据库/服务依赖和项目脚本。只有在这些信息明确后才安装依赖。

**第 3 步：安装或同步依赖。** 只选择与项目匹配的一种命令：

```powershell
# Node.js：三选一，按锁定文件选择
npm ci
pnpm install --frozen-lockfile
yarn install --immutable

# Python：按第 5 节已确定的工作流选择
python -m pip install -r requirements.txt
python -m pip install -e .
uv sync
poetry install
```

不要将同一代码块中的多条命令全都执行。Node.js 只执行一种包管理器命令；Python 只执行一种环境管理器命令。使用 pip 时，依赖安装后执行 `python -m pip check`；使用 uv 或 Poetry 时分别用 `uv run <命令>` 或 `poetry run <命令>` 执行后续命令。

**第 4 步：补齐本地配置。** 先检查是否提供了示例环境变量文件：

```powershell
Test-Path .env.example
Test-Path .env
```

仅当 `.env.example` 存在且 `.env` 不存在时，复制它并在编辑器中填写自己的非共享配置：

```powershell
Copy-Item -LiteralPath .env.example -Destination .env
```

随后按 README 启动所需的本地数据库、容器或迁移。`.env`、真实 API Key、令牌和账号密码不得提交；再次执行 `git status`，确认它们没有进入暂存区。

**第 5 步：运行项目已定义的质量检查。** 先列出脚本或测试配置，再只运行确实存在、且 README 要求的命令：

```powershell
# Node.js 项目：使用实际选定的包管理器
npm run
pnpm run

# Python 项目：选择与第 3 步相同的环境管理器
python -m pytest
uv run pytest
poetry run pytest
```

若 `lint`、`test`、`build`、`format` 等脚本存在，可依次运行对应的 `<包管理器> run lint`、`<包管理器> test`、`<包管理器> run build`。命令报错时先保留完整输出、定位第一个错误，再修复；不要用关闭检查或删除锁定文件的方式让命令“通过”。

**第 6 步：启动并人工走通主流程。** 按 README 的开发启动命令运行项目（常见形式为 `<包管理器> run dev`、`uv run <命令>` 或 `poetry run <命令>`），记录终端输出的本地地址。用浏览器或客户端完成一次核心操作，检查控制台、网络请求和保存结果；结束本地服务时按 `Ctrl+C`。准备演示时，再由另一位成员或无痕窗口重复一次主流程。

常见工具：

- JavaScript/TypeScript：ESLint、Prettier、Vitest/Jest。
- Python：Ruff、Black、Pytest。
- Git hooks：Husky（Node）或 pre-commit（Python）。先看仓库 README，再安装，避免擅自改变团队工作流。

黑客松的最低验收不是“功能很多”，而是 Demo 主流程可稳定运行。活动前和提交前都应由另一位成员在自己的电脑或无痕浏览器中走一遍：启动项目、完成核心操作、检查展示数据与链接。若项目依赖外部 API 或网络，准备演示用的备用数据、截图或短视频，但不要把备用方案当作未经验证的主流程替代品。

# 8. Windows 一次性检查清单

在新 PowerShell 窗口按项目实际技术栈执行以下检查；不使用的工具不需要安装，也不应以“找不到命令”为故障。每次安装后都先关闭并重新打开终端，再检查版本。

```powershell
# 所有 Git 项目
git --version
git config --global --get user.name
git config --global --get user.email

# 仅在使用 GitHub SSH 地址时
ssh -T git@github.com

# 编辑器与 AI 工具
code --version

# Python 项目
python --version
py --version
python -m pip --version

# Node.js 项目
node --version
npm --version

# 仅在 pnpm 项目中
pnpm --version
```

接着实际打开项目根目录，确认编辑器能打开文件夹。不要以本清单是否全部成功作为完成标准，而应以当前项目的 README 所列工具和版本为准。

进入实际项目根目录后，再额外检查：

```powershell
git status
git remote -v
```

黑客松赛前还应确认：AI Coding 工具已登录且可用、GitHub/GitLab 等团队仓库可访问、团队每位开发者至少能拉取与推送一次、项目的启动命令已在一台真实电脑上跑通，以及所需 `.env`/本地服务已按 README 配好。只安装项目真正会用到的工具即可。

# 9. Windows 推荐安装顺序

1. Windows Update、`winget` 与 Windows Terminal；赛前检查网络、充电和必要账号登录。
2. Git、GitHub SSH 密钥、编辑器与至少一种 AI Coding 工具；用一次小改动验证工具可用。
3. 安装编辑器与一种获准使用的 AI Coding 工具，完成登录、项目访问范围确认和一次小改动的人工审查。
4. 根据团队选定技术栈安装 Python 与唯一的环境管理方式，或 Node.js LTS 与项目所需的唯一包管理器；不必两者都装。
5. 建立团队仓库，按 README 配置环境变量和本地服务，依次跑通依赖安装、检查、测试、构建与启动，并验证每位成员可拉取和推送。

# 10. macOS 简明指南

## 10.1 需要的工具

按项目技术栈准备即可：**Terminal（zsh）**、Xcode Command Line Tools、Git、VS Code 或团队指定编辑器；Python 项目需要 Python 3 与一种依赖工作流（pip、uv 或 Poetry），Node.js 项目需要 Node.js LTS 与项目指定的包管理器。不要因为本节列出了工具就全部安装。

## 10.2 首次设置

1. 打开 **Terminal**，确认系统架构与命令行开发工具：

   ```bash
   uname -m
   xcode-select -p
   ```

   若第二条命令失败，执行 `xcode-select --install`，完成系统提示的安装后重新打开 Terminal。不要在 Apple Silicon 电脑中混用 Intel/Rosetta 与原生 Homebrew 路径。
2. 检查 Homebrew：

   ```bash
   brew --version
   ```

   若找不到 `brew`，从 [Homebrew 官方安装页](https://docs.brew.sh/Installation) 安装，并执行安装器输出的 shell 配置步骤；重新打开 Terminal 后再次运行 `brew --version`。只安装项目实际需要的工具，例如：

   ```bash
   brew install git
   brew install python
   ```

   Node.js 版本必须符合项目的 `.nvmrc` 或 `package.json`；若项目要求特定 LTS，不要仅因 Homebrew 提供 `node` 就默认安装它，按团队指定的版本管理方式准备。

3. 安装 VS Code 后，按 `Cmd+Shift+P`，运行 **Shell Command: Install 'code' command in PATH**；关闭并重新打开 Terminal，再验证：

   ```bash
   code --version
   ```

4. 验证已安装的运行时；Python 在 macOS 中使用 `python3`：

   ```bash
   git --version
   python3 --version
   python3 -m pip --version
   node --version
   npm --version
   ```

## 10.3 与 Windows 不同的命令

- Git 身份、分支协作、README/锁定文件判断、Node.js 包管理器选择与第 3、5.2、6、7 节相同；路径改用正斜杠，例如 `~/source/my-project`。
- GitHub SSH 流程按 3.3 执行；复制公钥时使用 `pbcopy < ~/.ssh/id_ed25519.pub`，而不是 `Set-Clipboard`。
- pip 工作流创建/激活虚拟环境时使用：

  ```bash
  python3 -m venv .venv
  source .venv/bin/activate
  python -m pip install -r requirements.txt
  ```

  uv 与 Poetry 的 `uv sync`、`uv run ...`、`poetry install`、`poetry run ...` 命令与 Windows 相同。不要在同一项目混用这些工作流。
- 提交前仍按第 7 节运行项目定义的检查、测试和启动命令；没有必要安装或使用 Windows Terminal、`winget`、`py` 或 PowerShell 执行策略。

# 11. Linux 简明指南

## 11.1 需要的工具

准备系统自带的终端（bash/zsh）、Git、Python 3 与 `venv` 支持、VS Code 或团队指定编辑器；Node.js 项目另需 Node.js LTS 与项目指定的包管理器。安装系统软件通常需要 `sudo` 权限；Python 项目依赖必须装进项目环境，绝不使用 `sudo pip` 或 `--break-system-packages`。

## 11.2 首次设置

1. 先识别发行版和包管理器：

   ```bash
   cat /etc/os-release
   ```

2. 使用**发行版对应的唯一包管理器**安装基础工具。以下是 Debian/Ubuntu 的示例；Fedora/RHEL 使用 `dnf`，Arch 使用 `pacman`，软件包名称请以发行版文档为准：

   ```bash
   sudo apt update
   sudo apt install git python3 python3-venv python3-pip
   ```

   仅当发行版提供的 Node.js 版本符合项目要求时才额外安装 `nodejs` 与 `npm`；否则使用团队批准的 Node 版本管理方式。不要同时安装多个全局 Node 版本管理器。
3. 验证基础工具：

   ```bash
   git --version
   python3 --version
   python3 -m pip --version
   ```

   若项目需要 Node.js，再执行 `node --version` 与 `npm --version`。Ubuntu/Debian 若提示不能创建虚拟环境，确认第 2 步已安装 `python3-venv`。
4. 安装编辑器时按 [VS Code Linux 安装说明](https://code.visualstudio.com/docs/setup/linux) 选择与发行版匹配的 `.deb`、`.rpm`、Snap、Arch 或其他方式。安装后执行 `code --version`；若找不到命令，重新打开终端并检查 `$PATH`。

## 11.3 与 Windows 不同的命令

- Git 身份、SSH、依赖文件的工作流选择、Node.js 包管理器判断和项目验证分别直接按第 3、5.2、6、7 节执行。SSH 公钥可用 `cat ~/.ssh/id_ed25519.pub` 显示后复制；不要泄露私钥。
- pip 工作流使用 POSIX 虚拟环境命令：

  ```bash
  python3 -m venv .venv
  source .venv/bin/activate
  python -m pip install -r requirements.txt
  ```

  激活后 `python` 指向 `.venv` 中的解释器；完成后运行 `deactivate`。uv 与 Poetry 的命令与 Windows 相同，并各自管理项目环境。
- 路径使用 `/home/你的用户名/source/项目名` 或 `~/source/项目名`；不要在 `/usr`、`/etc`、`/opt` 等系统目录中创建项目或 `.venv`。每次拉取或修改后，仍按第 7 节的顺序同步依赖、配置 `.env`、运行检查/测试，并验证启动流程。

# 官方参考

- [WinGet install 命令（Microsoft Learn）](https://learn.microsoft.com/windows/package-manager/winget/install)
- [Git for Windows](https://git-scm.com/install/windows)
- [GitHub：邀请协作者](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/inviting-collaborators-to-a-personal-repository)
- [GitHub：克隆仓库](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)
- [VS Code on Windows](https://code.visualstudio.com/docs/setup/windows)
- [Python on Windows](https://docs.python.org/3/using/windows.html)
- [Homebrew 安装说明](https://docs.brew.sh/Installation)
- [VS Code on macOS](https://code.visualstudio.com/docs/setup/mac)
- [VS Code on Linux](https://code.visualstudio.com/docs/setup/linux)
- [Python `venv`（含 macOS/Linux 激活命令）](https://docs.python.org/3/library/venv.html)
- [Ubuntu Python 虚拟环境指南](https://documentation.ubuntu.com/ubuntu-for-developers/tutorials/python-use/)
- [GitHub SSH 密钥（macOS/Linux）](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
