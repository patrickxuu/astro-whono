---
{
  title: 微软是个烂软件公司,
  date: 2026-11-25,
  tags: [ 微软, 体验 ],
  draft: false,
  archive: true,
  badge: 体验
}
---

> The only problem with Microsoft is they just have no taste.
>
> <cite>— Steve Jobs </cite>

其实也可以把上面这段话作为此文标题：**微软唯一的问题是完全没有品味**。

先解释一下我认为的“品味”标准：有统一的跨平台体验、用户交互统一且友好、设计风格完整、后续维护可信赖。

既然一开篇我们就引用了乔帮主的访谈，那就先总结几点我认为微软在“品味”上还有很多路要走的地方（主要相比苹果和一部分 Linux），然后后文里我会通过几个实例进一步说明这些：

- UI 设计割裂、官方规范无用，
- 用户交互体验糟糕，
- 系统维护升级体验糟糕，
- 没有统一的订阅管理页面、软件安装体验差，
- 盲目拥抱 AI，产品线规划一坨。


## UI 设计规范

这部分的 UI 设计主要指向目前 Windows 11 下的 WinUI 3，具体内容展示可参考下面这个 GitHub 仓库。

[![GitHub](https://img.shields.io/badge/GitHub-microsoft%2FWinUI--Gallery-181717?logo=github&logoColor=white)](https://github.com/microsoft/WinUI-Gallery)

<figure class="figure">
  <img src="/images/archive/microsoft-software-paradox/00.png" alt="WinUI Gallery Screenshot" />
  <figcaption class="figure-caption">WinUI Gallery Screenshot</figcaption>
</figure>

我个人认为，开发者应当主要遵从各平台独自的设计规范。从最近 iPhone Duo 的适配可以看出，厂商是希望软件开发者基于各平台的设计规范走的（不讨论那些平行视界的过渡方案，这些只会让软件厂商懈怠不想好好适配），如果所有开发者都可以基于 iOS 的设计规范，那么根本不会存在这么多完全无法适配 Duo 的状况存在。

本人去年做过很长时间的 Windows WinUI 应用开发，可以说 WinUI Gallery 应该是目前最符合微软设想中的 WinUI 3 样式的应用了。其实客观的说，WinUI 3 是个相当好看的设计样式，在经过微软前前后后多次完善后，目前的开发是基本没有问题的。但是，除了这个以外，各位还能看到多少遵守此规范的应用呢？这就不得不提到微软干的最离谱的东西了，过分依靠 WebView 套壳！

如何判断现在使用的软件是否为 WebView 套壳呢？其实相当容易，打开任务管理器，展开当前这个应用的详细情况，只要里面有和 WebView 沾边的条目就没跑了。然后我们就会惊喜的发现：

<figure class="figure">
  <img src="/images/archive/microsoft-software-paradox/01.png" alt="全新照片应用以及奇差的性能和内存占用" />
  <figcaption class="figure-caption">全新照片应用以及奇差的性能和内存占用</figcaption>
</figure>

<figure class="figure">
  <img src="/images/archive/microsoft-software-paradox/02.png" alt="全新的照片应用" />
  <figcaption class="figure-caption">微软全新的照片应用：网页套壳！</figcaption>
</figure>

如上图所示，微软最新推出的“照片”应用，依旧是网页套壳，甚至拥有奇差无比的性能表现。当你浏览全新的图库时，内存可以轻轻松松冲到 2 GB 占用（如果你像我一样试图高强度浏览 iCloud 图库，此时照片和后台同步进程一并的内存占用可以达到 **20 GB**！对，你没有看错）并且让你显卡瞬时占用跑到 20% 往上……

不仅仅是这个照片应用，微软目前的 Outlook、天气统统都是网页套壳……其实现在最尊重微软 WinUI 规范的大厂已经要变成苹果了（真就俩人是互相最好的软件开发者：微软的 Outlook 早早就适配了苹果的液态玻璃）。

回到我们日常使用的应用，如果我们尝试严格筛选符合 WinUI Gallery 呈现的设计风格的应用，会发现……几乎压根不存在！随便提几个名字吧，微信、网易云音乐是 Electron，QQ 是基于的 NT。

甚至更加喜闻乐见的，Windows 11 最新版本中仍然有大量新旧 UI 共存的情况。上至古早时期的 Windows 3.X，到不久之前的 Windows 10，你都可以轻松在 Win 11 中找到相关痕迹。很多人会说这是微软强大兼容性的证明，但这又何尝不是一种巨大风险的存在呢。

为了防止说我们只怼微软，我们就来看看苹果在 macOS 上的做法。可以随意翻翻 App Store 上的屏幕截图预览，我们也能够发现：虽然不是所有应用都遵循完整的 macOS 27 风格，但是至少大部分应用都对液态玻璃的控件进行了适配。反观微软这里，连自家应用都不肯全部适配一遍 WinUI 3 风格控件……

……三个字总结这部分：没救了！……


## 系统维护升级体验

这里也还是先从本人经历说起哈：本人从 2019 年加入 Windows 预览体验计划，经历了从 Win 10 19H1 到当下的 Win 11 26H2，这之中也完整经历了 Windows 11 的诞生。

<figure class="figure">
  <img src="/images/archive/microsoft-software-paradox/03.jpg" alt="Windows 预览体验计划" />
  <figcaption class="figure-caption">来自 2019 年的 Windows 预览体验计划</figcaption>
</figure>

本人实在是不明白微软最近着了什么魔。不知道和谁学来的新内容分批推送。说难听的小米澎湃系统的内测更新至少只要你有相应账号权限，该更新的新功能一个不少都给你。你微软本来版本号就有五位又五位的（现在我的是 26300.10075），每个版本可能都有自己的新功能要单独开启。难道你是在学习微信嘛？疯狂问号？

别和我提那个 ViVeTool，真的想不到一个系统开启新功能需要另一个开源脚本通过一串命令来开启（例如：New Modern Run Box 一个新功能需要 vivetool /enable /id:57156807,57259990,58381341,58527096 这样一长串来启用）。

理应来说，这个操作是最适合微软用上文提到的 WinUI 来设计一个统一的功能启用入口并且集成到系统中的，你大可以通过文字告诉用户此新功能的用途和预览风险。而绝非让用户天天使用这么一串意义完全不明的命令来启用……当然啦，似乎微软在其他实验性频道内实现了这一入口，可我们正式版预览通道完全没见到过，至少到目前想要一个新功能还是只能通过查博客就为了找这么一串乱码数字……

说到新功能，大家可能知道 Windows 11 在 26H2 冬季更新版本中大致更新了任务栏停靠位置和大小自定义、开始菜单更完整的个性化支持、WinUI 现代运行对话框、现代搜索界面。从我的措辞你也能够感觉到，这些功能理应是微软在 Windows 11 的第一个版本就提供的内容，却被拖了整整 5 年……甚至已经来到了 AI Agent 飞速发展的当下……微软你到底有多少阿三工程师啊。


## 软件安装、订阅管理体验

首先，软件安装体验：Microsoft Store 与独立安装程序体验严重割裂。

这个问题在过去都压根没必要提，当然是因为以前的 Microsoft Store 更加烂。只能安装那少得可怜的 UWP / WinUI 应用，从这里也可以看出开发者有多不喜欢微软的设计规范了。自从 Microsoft Store 引入了大量传统桌面版应用后，下面这种情况会越来越常见：

<figure class="figure">
  <img src="/images/archive/microsoft-software-paradox/04.png" alt="PowerToys" />
  <figcaption class="figure-caption">两个渠道安装的 PowerToys 无法直接互通</figcaption>
</figure>

PowerToys 应该说是目前微软比较重视的官方开源项目了。本人通过官方在 GitHub 仓库发行的 .exe 文件安装此软件，但如上图所示：通过 .exe 渠道安装和 Microsoft Store 渠道完全不互通。已经正常安装上的应用在 Microsoft Store 依然会显示未安装过。后续的软件更新自然也无法通过 Store 统一管理。

并且，在图中也可以发现，Store 版本的备注了“由 Microsoft 提供、更新并管理”。但如果使用过 winget 安装应用的话，很容易发现微软有能力统一管理电脑上几乎所有应用（包括常用的微信等）的更新。

<figure class="figure">
  <img src="/images/archive/microsoft-software-paradox/05.png" alt="winget" />
  <figcaption class="figure-caption">通过 winget 可直接管理所有应用更新</figcaption>
</figure>

我相信 winget 会慢慢成为 Windows 安装应用的一大主流渠道。毕竟我们这片土地上的软件厂商早已给了我们大量教训，你永远不知道安装过程中的下一步到底是什么意思，到底是垃圾软件全家桶还是什么未知的问题。而大部分 macOS 的应用安装非常有趣味，打开安装包后拖动到 Application 即可。微软！你能不能好好学学！！

其次是软件订阅管理体验，这一点可能是比较有争议的。我认为还是由于国人习惯了采用微信、支付宝来管理自动续费的服务，但其实有一个系统级的订阅管理是非常有必要的。

订阅管理目前做的好的我认为只有苹果系统（当然华为后续相当有实力能够追上），至于其他国内各家的安卓系统级支付已经被各种借贷、网贷占满了，个人对他们持悲观态度……

<figure class="figure">
  <img src="/images/archive/microsoft-software-paradox/06.jpg" alt="苹果跨平台的服务订阅管理页面" />
  <figcaption class="figure-caption">苹果跨平台的服务订阅管理页面</figcaption>
</figure>

这部分微软实现的仅仅只有能够管理 Office 订阅，并且仅仅只有网页端版本（Windows 系统设置里只有一个订阅的超链接指向网页端）。我认为这是完完全全不足的，和上面的软件安装体验一并构成了 Windows 上奇烂无比的软件管理体验以及大量无法管理的垃圾软件。


## AI 时代下混乱的产品线

<figure class="figure">
  <img src="/images/archive/microsoft-software-paradox/07.jpg" alt="Copilot" />
  <figcaption class="figure-caption">微软正在把一切都变成 Copilot</figcaption>
</figure>

一图以蔽之，微软正在把一切都变成 Copilot。这一混乱的 Copilot 产品线只是微软为了疯狂迎合 AI 而导致的恶果。

让我们来看看微软在 Win 11 中实装了哪些 AI 功能。单击以执行、回顾、AI 集成的搜索、AI 集成的文字提取，当然啦，最没用的应该还是键盘上的 Copilot 实体键（相信很多人电脑键盘上因为这个键的存在缺少了右 Ctrl 键）。由于我的游戏本搭载了 AMD Ryzen AI 9 HX 370 处理器，50 TOPS 的 NPU 使我能够使用上述所有 AI 功能。但是很明显，里面最有用的只有 AI 集成的文字提取功能，其他的完全处于噱头大于实际价值的阶段……

这完全不是苹果那种 Apple Intelligence，其与系统高度集成，各类功能可以相当无缝的融入系统体验：你可以在各处输入时调用 AI 润色、可以在大量消息通知席卷时轻松使用 AI 摘要、可以与系统相册得到完全一致性的体验。种种这些，在微软当下的 Windows 11 都是天方夜谭，即使是所谓主推的 Copilot+ PC。

说到产品线规划，再同步一个最新 bad news 吧：

> IT之家 11 月 19 日消息，据IT之家小伙伴反馈，微软官网发布公告，Microsoft To Do 将于 2027 年 6 月 30 日停用，包括网页版、Windows、Mac、iOS 和 Android 客户端。

微软砍刀部你坏事做尽！


## 总结

UI 设计规范、用户交互体验、系统维护升级体验、统一的订阅管理页面、软件安装体验、良好的产品线规划，这些理应来说是一个现代的完整的操作系统该做到的。但我们的微软却完美的避开了所有正确答案，并且在与用户背道而驰的路上越走越远。微软毫无疑问是一家伟大的商业公司，但是在体验与品味方面实属无法苟同。

回到开头乔帮主的那句话：**“The only problem with Microsoft is they just have no taste.”** 我还是坚定的认为目前能够达到有“品味”标准的还是有且仅有苹果一家系统。

言尽于此，我们实在是没办法相信微软能够在可预见的未来甚至是 Windows 12 中大幅改善这些情况，还是寄希望于华为鸿蒙系统能够在这“品味”方面上努力追赶上吧。