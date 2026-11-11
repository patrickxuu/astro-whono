---
{
  title: 微软开源 Windows Developer Config，体验一条命令，让 Windows 开箱即编码,
  date: 2026-11-12,
  tags: [ 微软, 开源, 体验 ],
  draft: false,
  archive: true,
  badge: 体验
}
---

前段时间，微软发布名为 Project Zenith 的新系统，该系统面向开发者提供开箱即编码的 Windows 11 PC 体验。当然说是新系统其实就是在 Windows 11 基础上进行优化改进，例如预装常用开发工具以及关闭某些可能影响开发者日常使用的无关功能。但是一提到新系统，这就来到了微软的传统艺能，也就是只有满足该项目的软硬件要求才能被称为 Project Zenith 设备。而要满足硬件要求，设备至少配备 64GB 内存、内存带宽达到 250GB / 秒且必须配备 AI 处理器或附带 NPU 单元。

<figure class="figure">
  <img src="/images/archive/experience-windev-config/00.jpg" alt="Project Zenith" />
  <figcaption class="figure-caption">Photo credit: Landian.News</figcaption>
</figure>

Project Zenith 项目想必是需要肥马轻裘的家庭条件才能够拥有🤔。但好消息是，实际上 Project Zenith 相关体验也可以通过微软维护的开源 [Windows Developer Config](https://github.com/microsoft/WindowsDeveloperConfig) 实现，也就是启用 Windows 11 默认并未开启的开发者功能，配置完成后与 Project Zenith 并没有太大的区别。

今天就让我们来体验一下这一微软官方开源脚本吧。

先放出此开源项目的基本信息，欢迎大家多多 Star，助力微软继续加油产出（不得不说微软其实非常明白用户需求，从这次的项目到 [PowerToys](https://github.com/microsoft/PowerToys) 都可见一斑。但是又能够长期在 Windows 11 上不作为，放任 Webview 之流盛行于世，属实是没什么办法了😓）：

[![GitHub](https://img.shields.io/badge/GitHub-microsoft%2FWindowsDeveloperConfig-181717?logo=github&logoColor=white)](https://github.com/microsoft/WindowsDeveloperConfig)

> 其实主包个人非常喜欢这一类脚本工具。作为一个经常因为环境配置而重装系统的人，有一个不及预期的开发环境真的会疯掉的。这种时候这样的一站式解决方案其实相当不错，至少可以快速帮你在开发环境配置与美观性上达到平衡。这次体验也是为主包下次重装系统做一下前期准备。

## 前期准备

由于主包的电脑已经被各路开发环境占据，不太能体现此脚本的完整执行流程，故本次体验先在虚拟机中进行。

| 环境配置 | 内容 |
| --- | --- |
| 虚拟机版本 | VMware® Workstation Pro 26H1 |
| 虚拟机系统 | Windows 11 2026 更新 版本 26H2 |
| 内存分配 | 6 GB |
| CPU 分配 | AMD Ryzen AI 9 HX 370 (8C) |
| 硬盘分配 | 64 GB NVMe |

> 微软居然在 26H2 又堵死了这么多跳过 OOBE 登录的办法，真是坏事做尽……😭

## Windows Dev Config 部分

### 主要内容

- **开发工具：** Windows Terminal、PowerShell 7、Git、GitHub CLI、GitHub Copilot CLI、VS Code、.NET SDK 10、Python 3.14 + uv、Node.js LTS + nvm、Coreutils for Windows、Windows App CLI、Oh My Posh 和 PowerToys。
- **终端：** 将 PowerShell 7 设为默认配置文件，在提示符中使用 Oh My Posh，将 Cascadia Mono NF 设为默认字体，并在下拉菜单中添加 GitHub Copilot 配置文件。
- **Windows 设置：** 深色主题、长路径、文件资源管理器默认设置、开始/搜索设置以及勿扰模式，开发者模式、Sudo、关闭小组件以及 Edge 策略，额外的开始/搜索/系统托盘设置。
- **WSL：** WSL 平台 + Ubuntu，包括重启以及之后的自动恢复。
- **远程桌面：** 启用并设置防火墙规则。

### 配置步骤

1. 在 Windows 终端 PowerShell 选项卡中输入并执行：
```
irm https://aka.ms/devconfig/full/setup.ps1 | iex
```
2. 随后会要求获取管理员权限，便会进入脚本初始化阶段（微软称之为：Calm OS setup）。这一步会优先完成 PowerShell 7 的安装，以便后续 WinGet 脚本的实现。
   
<figure class="figure">
  <img src="/images/archive/experience-windev-config/01.png" alt="脚本初始化阶段" />
  <figcaption class="figure-caption">脚本初始化阶段</figcaption>
</figure>

3. 此时会依次完成 11 阶段的内容安装，并且包含一次系统重启。这里将会列出 11 个阶段的主要内容以及屏幕截图供参考：

| 安装阶段 | 大致内容 | 屏幕截图 |
| --- | --- | --- |
| Getting ready | 配置和更新 WinGet 模块 | [1/11](/images/archive/experience-windev-config/02.png) |
| Packages | 安装上述各开发工具 | [2/11](/images/archive/experience-windev-config/03.png) |
| System settings | 配置系统策略与远程桌面规则 | [3/11](/images/archive/experience-windev-config/04.png) |
| File Explorer tweaks | 配置文件资源管理器 | [4/11](/images/archive/experience-windev-config/05.png) |
| Taskbar, search & start tweaks | 额外的开始/搜索/系统托盘设置 | [5/11](/images/archive/experience-windev-config/06.png) |
| Microsoft Edge tweaks | 配置 Edge 策略 | [6/11](/images/archive/experience-windev-config/07.png) |
| Fonts | 配置默认终端字体 | [7/11](/images/archive/experience-windev-config/08.png) |
| Windows Terminal | 设置终端默认配置文件 | [8/11](/images/archive/experience-windev-config/09.png) |
| PowerShell profile | 配置 OhMyPosh | [9/11](/images/archive/experience-windev-config/10.png) |
| GitHub Copilot | 添加 GitHubCopilot | [10/11](/images/archive/experience-windev-config/11.png) |
| WSL + Ubuntu | 安装 WSL 和发行版 | [11/11](/images/archive/experience-windev-config/12.png) |

整个过程全程需要互联网连接（再加上稳定的代理当然就更好了），在第二阶段会下载大量软件包（耗时久、可以注意下流量消耗），在最后一阶段结束后会安排一次系统重启。

### 大致体验

在一台全新安装的 Windows 11 26H2 虚拟机上，完成上述内容安装大致会增加 6GB 的存储占用。

<figure class="figure">
  <img src="/images/archive/experience-windev-config/13.png" alt="安装后体验预览" />
  <figcaption class="figure-caption">安装后体验预览</figcaption>
</figure>

个人非常喜欢这里面的智能终端（垂直标签页的风终于吹到了 Windows 终端）以及新的终端主题。当然啦，诸如 Git、VS Code、Python、Node.js 这些开发工具还有 PowerToys 自不必多说，有这样一个一站式的官方解决方案真的能很大程度上节约重装系统后的时间开销。

## WSL Comfort 部分


## Workloads 部分

