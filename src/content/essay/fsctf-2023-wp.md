---
{
  title: FSCTF 2023 校内赛道 WP,
  date: 2023-10-22,
  tags: [ CTF, WP ],
  draft: false,
  archive: true,
  badge: WP
}
---

ID：helloxuh

分数：6696

解题数：19

-----

2026 年作者注：此解题文档是根据作者大一当时比赛后提交的 WriteUP 文档改编而来，放在如今看可能意义不大，不过作为当时依然热爱过 CTF 和不断学习网安知识的青春记忆，故把这些一并放在网站中留存。在那个 AI 都还远没有井喷式发展的年代，自己原来真的可以做到如此高强度的疯狂检索学习吸收这些内容，确实也是一段非常青春的回忆了……若后续本人还有 CTF 题目或者其他算法刷题的题解，也会继续沿用这些 tag 更新在网站中。


## WEB - 源码！启动！

先看题目：“源码”提示可能需要查看网页源代码。

![WEB-1.png](https://s2.loli.net/2023/10/22/imOvkIunYyrs5T1.png)

开启环境后，发现鼠标右键和键盘 F12 键均被禁用。因此这里选择通过浏览器的选项进入开发人员工具。

![image.png](https://s2.loli.net/2023/10/22/D1thv4B7jWzTJoi.png)

得到 Flag 为 **NSSCTF{a46d9aca-2c18-4d6f-b636-ec4a71542e83}** ，解题完成。


## WEB - Hello, you

先看题目，提示与 RCE 有关。

![image.png](https://s2.loli.net/2023/10/22/Uf4osNJ3lkRj6Wv.png)

![image.png](https://s2.loli.net/2023/10/22/wT5GJmPZtQFIxyX.png)

开启环境后，在源码中发现几段命令注入的语句提示。在用户名输入框中测试：

1&&ls		能够正常显示结果，发现目录下存在 flag.php 和 index.php 两个文件。

1&&cat flag.php		提示非法操作，猜测有关键词过滤。

1&&ca\t fl\ag.php		正常显示 Flag 内容为 **NSSCTF{408900e5-67bf-4c99-bd4f-34e75a6e7f22}** ，解题完成。

复盘 index.php 文件内容，1&&ca\t ind\ex.php，可以看出过滤的具体语句。

![image.png](https://s2.loli.net/2023/10/22/NY71ngKox3Hdav5.png)


## WEB - webshell 是啥捏

先看题目，只发现题目有 webshell 提示，不清楚用途。

![image.png](https://s2.loli.net/2023/10/22/OYb9xWvn1eSQ7BH.png)

开启环境后，发现一份 php 代码，且在源码中未发现有效信息。

![image.png](https://s2.loli.net/2023/10/22/tl5Tv9BPCVxpQ4Y.png)

*这题与下一题 **签到 plus** 的步骤有相似之处，故放在一起说。*


## WEB - 签到 plus

先看题目，发现信息“被黑客接管”，根据以往刷题经历判断出目录中存在 shell.php 文件。

![image.png](https://s2.loli.net/2023/10/22/nKBp29hDMmZQ6ge.png)

开启环境后，在 URL 中加入 /shell.php ，观察网页信息，得到 PHP 版本为 7.4.21。通过搜索得知此版本存在一个漏洞。

开始复现漏洞。BurpSuite 抓包丢到重放器并且关闭重放器的自动修改 Content-Length 选项。

修改请求头为（需包含所以换行符）：

```http
GET /phpinfo.php HTTP/1.1
Host: pd.research


GET / HTTP/1.1

```

开始放包。即可得到一串 php 代码，其格式与上一题完全相同。

代码中的 `if (isset($_GET['']))` 表示判断方括内的变量是否存在，因此解题关键在于传参传入一个同名的变量。

上一题可直接复制 emoji 表情至 URL 中，而本题可以在 wxMEdit 中得到 Unicode 编码后转为 emoij 表情传入 URL。

通过以上操作即可解题。


## REVERSE - MINE SWEEPER

先看题目，没有什么收获。

下载附件打开后，还是没发现什么有用信息。

尝试在 IDA 中打开，Shift+F12 后，得到 Flag 为 **FSCTF{We1C0m3 t0 rev w0r1d!!!}** ，解题完成。

![image.png](https://s2.loli.net/2023/10/22/Vwn53pCetPJEvqa.png)


## REVERSE - ez_pycxor

先看题目，没有什么收获。

下载附件后，得到一个 .pyc 文件。因为之前有过 Python 反编译的实践经历。

所以直接打开自己之前做的工具整合包，这里用到了 pycdc.exe 工具。

![image.png](https://s2.loli.net/2023/10/22/2cjM7zvoXYGJwWm.png)

得到反编译后的 Python 源码。在经过简单的逆向后，有以下代码。

得到 Flag 为 **FSCTF{8a3ccd61ab7ff9e87acb9c9d1}** ，解题完成。

![image.png](https://s2.loli.net/2023/10/22/HkglMQYWxwzIX5a.png)


## CRYPTO - RSA1

先看题目，没有什么收获。

下载附件后，得到 RSA 类型为已知 p, q, e 求 d，这里直接使用 Python 脚本完成。

![image.png](https://s2.loli.net/2023/10/22/Hq9lb4SaYcAfi6p.png)

得到 Flag 为 **FSCTF{5865518808244394324786753}** ，解题完成。


## CRYPTO - RSA2

先看题目，没有什么收获。

下载附件后，得到 RSA 类型为已知 p, q, c, e 求值，这里直接使用 Python 脚本完成。

![image.png](https://s2.loli.net/2023/10/22/IgnQ9kdOtAsmuPY.png)


## CRYPTO - RSA3

先看题目，没有什么收获。

下载附件后，得到 RSA 类型为已知 n, e, dp, c 求值，这里直接使用 Python 脚本完成。

![image.png](https://s2.loli.net/2023/10/22/eJ3DMFgvupnK5TO.png)


## CRYPTO - 做不出来就别阴阳怪气啦

先看题目，得到信息”阴阳怪气“。

（其实刚开始做的时候发现不了这个信息。可以复制一小段文本搜索即可得到阴阳怪气编码）

![image.png](https://s2.loli.net/2023/10/22/4Q7oJcW9XgmRpiU.png)

使用网络上的在线”阴阳怪气编码器“即可解出 Flag 为 **FSCTF{Jiuzhe@JustSoSo}** ，解题完成。

![image.png](https://s2.loli.net/2023/10/22/sU56uXzktWoCeM9.png)


## CRYPTO - 埃塞克的秘密

先看题目，得到信息：埃塞克可能为 ASCII 编码。

![image.png](https://s2.loli.net/2023/10/22/XUi2JwyAdmts7xH.png)

打开附件后，判断可能为十进制的 ASCII 编码。

通过在线 ASCII 转换器得到 Flag 为 **FSCTF{u$r%uL%9o?<0J@FN}** ，解题完成。

![image.png](https://s2.loli.net/2023/10/22/xNCGgE4YrmO1vUH.png)


## MISC - 改过自新，从头再来

签到题，在题干中得到 Flag 为 **FSCTF{WE1c0me_To_Fut^re_St@r_CTF}** ，解题完成。

![image.png](https://s2.loli.net/2023/10/22/aHeqFp1hYUjAwPD.png)


## MISC - SimpleEncryption

先看题目，得到信息”压缩包分析“。

![image.png](https://s2.loli.net/2023/10/22/ueDExAZUWBLwb9l.png)

附件下载完成后，开始以为是需要爆破压缩包密码，但尝试多次后无果。

尝试使用 Notepad3 打开压缩包文件，

![image.png](https://s2.loli.net/2023/10/22/XHGW4emFwukc2Y7.png)

得到 Flag 为 **FSCTF{Wei_Ji@mi_s0_EasY}** ，解题完成。


## MISC - 萧河

先看题目，

![image.png](https://s2.loli.net/2023/10/22/M9cI6HWakegohuj.png)

下载附件，附件为一个名为 png 的不带后缀的文件，结合题目提示猜测，缺少 png 头文件。

用 wxMEdit 打开，修改头文件格式 89 50 4E 47 并保存，得到一个图片文件，但发现图片不全。

再次结合题目提示，猜测图片大小被修改。在第二行找到 png 大小源码，将宽度值修改为与长度值相同。

打开图片，得到 Flag 为 **FSCTF{xiaojia_xiaohe}** ，解题完成。

![png _2_.png](https://s2.loli.net/2023/10/22/IKnPVtjhUciY1sy.png)


## MISC - 行不行啊细狗

先看题目，无信息。

![image.png](https://s2.loli.net/2023/10/22/FPDmMv9sYr6IBi8.png)

附件为一个 Word 文档，猜测有隐写存在。

![image.png](https://s2.loli.net/2023/10/22/fbrJj3C6mypEkdN.png)

这里选择将 docx 后缀改为 zip 格式打开，在目录 word 下打开 document.xml，找到两段 Flag 内容， FSCTF{N0t_A_heRo_和doEs_not_re@d_t 。在群里得到第三段 Flag 为 He_3_Kinggggdoms 。

拼接后得到 Flag 为 **FSCTF{N0t_A_heRo_doEs_not_re@d_tHe_3_Kinggggdoms}** ，解题完成。


## MISC - ez-osint

先看题目，根据图片解出拍摄时间。

![image.png](https://s2.loli.net/2023/10/22/AotmwW9OCu7MH3S.png)

附件为一张图片。得到以下信息：在国外，一辆公交车，公交车的车牌、车次，公交车上的广告（推测为类似泰语，推测在东南亚），一座建筑，阳光照射角度。

![27281696669078_.pic.png](https://s2.loli.net/2023/10/22/Rx9iCwWYZdky8Sj.jpg)

在尝试将这些信息在网上检索时，找到一篇文章。

![image.png](https://s2.loli.net/2023/10/22/xi9erJh1WEFKzGv.png)

通过文章中的解题方法得到 Flag 为 **FSCTF{08_40}** ，解题完成。


## MISC - base套

先看题目，未发现明显的提示信息。

![image.png](https://s2.loli.net/2023/10/22/HlpExFu1gh5kCo4.png)

打开附件后，发现可能为 Base64 编码的信息。通过在线 Base64 解码网站解码N多次后即可得到 Flag 内容。

![image.png](https://s2.loli.net/2023/10/22/BnflDUKmOAzTk3v.png)


## MISC - 先签个到吧

先看题目，得到信息：glan 的学校附近，一个纪念馆（很可能不是特别著名）。

![image.png](https://s2.loli.net/2023/10/22/LiFYoAl34KpXOUz.png)

对于信息 glan 的学校附件，在群里找到出题人备注为 TUT 即天津理工大学，通过地图网站查询附近地标。

![image.png](https://s2.loli.net/2023/10/22/MGIpB6DY3AyR4ad.png)

得到一处地点为霍元甲纪念馆，尚武休闲广场，精武门中华武林园附近。得到 Flag，解题完成。


## MISC - 夜深人静的时候也会偷偷emo

先看题目，无有效信息。

![image.png](https://s2.loli.net/2023/10/22/jhDiAGznawOPU3Y.png)

附件为一个带密码的压缩包，一开始猜测题干中的三点可能代指密码位数但无果。暴力破解，破解密码为 12345。

解压后得到一个 mp3 音频文件。

尝试使用 Audacity 观察波形图无果。

尝试使用 MP3Stego 解题，一开始无果。后面重发了 mp3 文件后再次尝试。

![image.png](https://s2.loli.net/2023/10/22/huM9rNzQvpie2Xw.png)

得到 Flag 为 **FSCTF{CemMEnt_Se@1s_tHe_heaaaaaart_foR_An0ther_D@y}** ，解题完成。


## FSCTF - 问题复盘

<figure class="figure">
  <img src="/images/archive/fsctf-2023-wp/00.png" alt="问题复盘" />
  <figcaption class="figure-caption">FSCTF - 问题复盘</figcaption>
</figure>

在赛题涉及的5个方向中，MISC 方向情况较好，PWN、REVERSE 方向比较一般。

有几道赛题解出一大半之后剩下几步无法继续完成，在这一点上会比较吃亏。

有几道赛题解法与官方 WP 完全一致，却无法实现，原因不明。

总体而言，这是我第一次参加 CTF 比赛，结果还是大体上令人满意的。
