# SYE-Engine

**Create games. Connected to your AI.**

**基于 Godot 的 AI 原生游戏开发工具，集 Hub、Editor、多语言开发与跨平台构建于一体。**

**An AI-native game development toolkit built on Godot, bringing together a Hub, an Editor, multiple programming languages, and cross-platform build workflows.**

[简体中文](#简体中文) · [English](#english)

---

## 简体中文

### 关于 SYE

SYE 是基于 **Godot 4.7.2** 深度扩展的独立游戏引擎发行版。它保留 Godot 的场景、资源、渲染和插件体系，在此基础上加入原生 AI 工具接口、统一语言环境、平台组件管理及增强的构建与导出流程。

你可以自己制作游戏，也可以让支持 MCP 的外部 AI 客户端直接参与制作：查询编辑器状态、创建场景、编写脚本、读取编译错误、运行并观察游戏，再生成可交付的构建。

**当前版本：`0.2.0-preview.2` · Hub 主机：Windows x64 · 上游基线：Godot `4.7.2-stable`**

### 主要能力

| 能力 | 说明 |
| --- | --- |
| **Editor 原生 MCP** | 外部 AI 可查询场景与节点、编辑场景、操作受支持资源和脚本、读取构建诊断、运行及观察游戏，并调用导出工具；提供限定文件范围的检查点与恢复能力，无累计调用次数配额。 |
| **四种开发语言** | 一个 Editor 支持 **GDScript、C#、C++ 和 TypeScript**。C++ 通过 GDExtension 接入；TypeScript 使用集成的 GodotJS-Ext / QuickJS 运行时，玩家无需安装 Node.js。 |
| **Hub 统一管理环境** | 管理项目、引擎、语言组件、平台模板和私有工具链，提供安装、修复和移除入口，按项目需要准备构建环境。 |
| **增强的导出流程** | 支持 Debug / Release；在支持的目标上提供 C# NativeAOT、TypeScript QuickJS Bytecode、PCK 合并和播放器库布局。具体能力取决于语言及目标平台。 |
| **Windows 生成 IPA** | 独立的“iOS 应用”导出入口，可在 Windows 生成 IPA，配套 Apple 账号、签名及 USB 设备安装工具；保留传统 Mac/Xcode 路线。安装到普通 iPhone 仍需要有效的 Apple 签名和设备授权。 |
| **StreamingAssets** | 固定使用 `Assets/StreamingAssets` 保存原始资源，隔离常规编辑器导入；导出时保留原始字节及目录结构，并提供统一读取接口。 |
| **更整洁的 Windows 成品** | 支持小型启动 EXE 配合播放器库，运行依赖统一放入 `Game` 目录；可合并 PCK，不能合并的运行库保留为外部文件。 |
| **集成运行与设备工具** | 游戏视图可内嵌在编辑器主区域，也可浮窗；提供 Android ADB 连接、安装、启动和应用日志，以及 iOS USB 安装入口。 |

MCP 是连接外部 AI 客户端的工具接口。本发行包不附带 AI 模型，也不包含第三方 AI 服务的订阅。

### 快速开始

1. 下载并解压完整发布包，保留整个文件夹结构。
2. 双击 **`SYEHub.exe`**。
3. 在 Hub 的引擎页面选择 **安装引擎**，然后选择需要的语言和平台组件。
4. 创建或导入项目，进入 SYE Editor。
5. 如需 AI 协作，在 Editor 的 MCP 面板获取连接配置，交给支持 MCP 的外部 AI 客户端。

配套 Editor 与 SYE 定制组件的安装包已经随文件夹提供，无需手工逐个解压。公共 SDK、编译器及其他构建依赖由 Hub 按所选组件联网下载；供应商有许可要求时，按安装界面提示确认。

**分发或移动时请复制整个文件夹，而不只是 `SYEHub.exe`。** 组件安装后还会占用额外磁盘空间，大小取决于所选语言和平台。

### 游戏目标平台

| 目标 | 当前范围 |
| --- | --- |
| **Windows** | 四语言开发与导出；Debug / Release、播放器库布局及适用语言的 AOT / 字节码流程。 |
| **Android** | APK / AAB 导出、签名及 ADB 设备工具。C# Android 仍属于实验性支持，具体设备和架构需要验证。 |
| **Web** | WebAssembly 导出。C# Web 是 SYE 的实验性扩展；多线程与部署要求以目标语言和导出提示为准。 |
| **Linux** | 已接入导出与相关交叉编译组件；成品需在目标系统验证。 |
| **macOS** | 保留相关导出流程；语言扩展、构建及签名要求取决于对应的 Mac 工具链。 |
| **iOS** | Windows 原生 IPA 路线与 Mac/Xcode 路线；语言、原生扩展、签名及目标设备要求分别处理。 |

**当前为开发预览版。** 平台入口可用不代表所有语言、插件、架构和设备组合均已完成验证。尤其是 C# Web、C# Android 及自定义原生扩展，应结合实际项目验证。

### 文件夹说明

```text
Hub/
├─ SYEHub.exe                 # 启动入口
├─ README.md                  # 中英文说明
├─ 使用说明.txt
├─ download-sources.json      # 集中管理的组件及公共依赖来源
├─ Packages/                  # Editor 与 SYE 组件安装包
├─ Licenses/                  # 许可证与第三方声明
└─ Metadata/                  # 版本、SHA256 与保护范围记录
```

这里提供的是便携式二进制发行包，不是完整的引擎源码仓库。发布程序对部分自有实现采用编译、加密或混淆保护；公开开发接口、必要模板和第三方对应源码按适用许可保留。**没有商业激活或收费授权校验。**

### 反馈与许可

提交 Issue 时，请附上 SYE 版本、目标平台、开发语言、复现步骤和相关日志。导出问题请同时说明 Debug / Release 及 AOT 等关键选项。

SYE 是独立项目，与 Godot、Unity 或 Apple 没有官方隶属或背书关系。感谢 Godot 社区及所有上游项目。

SYE 自有内容的许可见 [SYE-LICENSE.txt](Licenses/SYE-LICENSE.txt)，其中列出的例外及第三方组件遵循各自许可。Godot 许可与版权见 [GODOT-LICENSE.txt](Licenses/GODOT-LICENSE.txt) 和 [GODOT-COPYRIGHT.txt](Licenses/GODOT-COPYRIGHT.txt)；其他说明见 [THIRD_PARTY_NOTICES.md](Licenses/THIRD_PARTY_NOTICES.md) 及组件包内的声明。

---

## English

### About SYE

SYE is an independent game engine distribution built on **Godot 4.7.2**. It retains Godot's scene, resource, rendering, and plugin systems while adding native AI tooling, managed language environments, platform components, and extended build and export workflows.

Build games yourself, or bring an external MCP-compatible AI client into the workflow: inspect the editor, create scenes, write scripts, read compiler diagnostics, run and observe a game, and produce distributable builds.

**Current release: `0.2.0-preview.2` · Hub host: Windows x64 · Upstream baseline: Godot `4.7.2-stable`**

### Highlights

| Feature | What it provides |
| --- | --- |
| **Native Editor MCP** | External AI clients can inspect scenes and nodes, edit scenes, work with supported resources and scripts, read build diagnostics, run and observe games, and invoke export tools. Scoped file checkpoints and restoration are available, with no cumulative tool-call quota. |
| **Four programming languages** | One Editor supports **GDScript, C#, C++, and TypeScript**. C++ integrates through GDExtension; TypeScript uses the integrated GodotJS-Ext / QuickJS runtime. Players do not need Node.js. |
| **Managed environments through the Hub** | Manage projects, engines, language components, export templates, and private toolchains, with installation, repair, and removal workflows. |
| **Extended exports** | Debug / Release, C# NativeAOT on supported targets, TypeScript QuickJS Bytecode, embedded PCKs, and player-library layouts. Availability depends on the language and target platform. |
| **IPA generation on Windows** | A dedicated iOS Application export workflow generates IPA files on Windows, with Apple account, signing, and USB installation tools. The traditional Mac/Xcode route is retained. Installation on a standard iPhone still requires valid Apple signing and device authorization. |
| **StreamingAssets** | Keep raw assets in `Assets/StreamingAssets`, outside the normal editor import workflow. Exports preserve original bytes and directory structure, with a unified access interface. |
| **Cleaner Windows builds** | Use a small launcher EXE with a player library and dependencies under a consistent `Game` directory. PCKs can be embedded; runtime libraries that cannot be merged remain external files. |
| **Integrated play and device tools** | Embed the game view in the editor's main workspace or use a floating window. Android ADB tools cover connection, installation, launch, and application logs; iOS provides a USB installation workflow. |

MCP connects the Editor to an external AI client. This distribution does not bundle an AI model or include subscriptions to third-party AI services.

### Getting started

1. Download and extract the complete release, keeping its folder structure intact.
2. Run **`SYEHub.exe`**.
3. Open the engines page, choose **Install Engine**, and select the language and platform components you need.
4. Create or import a project and open it in SYE Editor.
5. For AI collaboration, obtain the connection configuration from the Editor's MCP panel and add it to an MCP-compatible AI client.

Installation packages for the matching Editor and SYE-specific components are included. There is no need to extract component archives manually. The Hub downloads public SDKs, compilers, and other build dependencies as needed; accept any applicable vendor terms through the installation workflow.

**When moving or sharing this release, copy the entire folder, not only `SYEHub.exe`.** Installed components require additional disk space depending on your language and platform selections.

### Game targets

| Target | Current scope |
| --- | --- |
| **Windows** | Four-language development and export, Debug / Release, player-library layouts, and applicable AOT / bytecode workflows. |
| **Android** | APK / AAB export, signing, and ADB device tools. C# Android remains experimental; device and architecture compatibility must be validated. |
| **Web** | WebAssembly export. C# Web is an experimental SYE extension; threading and deployment requirements depend on the language and export configuration. |
| **Linux** | Export and relevant cross-compilation components are integrated. Validate the resulting build on the target system. |
| **macOS** | Existing export workflows are retained. Language extensions, building, and signing depend on the corresponding Mac toolchain. |
| **iOS** | Windows-native IPA and Mac/Xcode workflows. Language support, native extensions, signing, and device requirements are handled separately. |

**This is a development preview.** An available platform workflow does not mean that every combination of language, plugin, architecture, and device has been validated. C# Web, C# Android, and custom native extensions in particular require project-specific validation.

### Package layout

```text
Hub/
├─ SYEHub.exe                 # Application entry point
├─ README.md                  # Chinese and English introduction
├─ 使用说明.txt
├─ download-sources.json      # Central component and dependency sources
├─ Packages/                  # Editor and SYE component installers
├─ Licenses/                  # Licenses and third-party notices
└─ Metadata/                  # Version, SHA256, and protection records
```

This is a portable binary distribution, not the complete engine source repository. Selected SYE implementations use compilation, encryption, or obfuscation for source protection. Public development interfaces, required templates, and corresponding third-party sources remain available under their applicable licenses. **There is no commercial activation or paid-license verification.**

### Feedback and licensing

When opening an issue, include the SYE version, target platform, programming language, reproduction steps, and relevant logs. For export issues, also specify Debug / Release and important options such as AOT.

SYE is an independent project and is not affiliated with or endorsed by Godot, Unity, or Apple. Thanks to the Godot community and all upstream projects.

See [SYE-LICENSE.txt](Licenses/SYE-LICENSE.txt) for SYE's own content, including the listed exceptions. Third-party components retain their respective licenses. Godot's license and copyright notices are in [GODOT-LICENSE.txt](Licenses/GODOT-LICENSE.txt) and [GODOT-COPYRIGHT.txt](Licenses/GODOT-COPYRIGHT.txt). Additional details are in [THIRD_PARTY_NOTICES.md](Licenses/THIRD_PARTY_NOTICES.md) and the notices included in component packages.
