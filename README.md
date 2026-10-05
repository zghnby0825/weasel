小狼毫自用分支，不定期可能rebase reset force push

如果觉得我瞎整的还不错，可以请我喝冰阔落🥤 :)

微信赞赏码

<img width="600" height="600" src="https://github.com/user-attachments/assets/503063b1-4951-4d88-aaa3-463585135233" />


本分支说明（自用）
------------------

Fork 自 [fxliang/weasel](https://github.com/fxliang/weasel) 的 `pb` 分支，在上游基础上只做了下面这些事：

* **重绘状态图标**：英文 `英`、中文 `中`、全角 `全`、半角 `半`、部署中 `↻`
  无框 · 白色字形 + 深灰描边 · 透明底（字形取自 MapleMono NF CN 的位图渲染），深浅背景下都看得清；
  源码即 `resource/*.ico`，六个尺寸档位 16/24/32/48/64/256（256 为 PNG 压缩，其余 32bpp DIB）。
* 其余行为与上游 `pb` 分支一致。

[![Personal Build](https://img.shields.io/github/v/release/zghnby0825/weasel?include_prereleases&label=personal%20build)](https://github.com/zghnby0825/weasel/releases)

自用构建（Personal Build）
--------------------------

| 项目 | 说明 |
| :-- | :-- |
| 发布页 | <https://github.com/zghnby0825/weasel/releases>（预发布版，不定期更新） |
| 构建环境 | Visual Studio 2022 生成工具 17.14 / MSVC 14.44（v143）/ Windows SDK 10.0.26100 / Boost 1.90.0 / librime 1.17.0 / NSIS 3.12 |
| 架构 | **x64 + x86**（暂未包含 ARM / ARM64 / ARM64X） |
| 代码签名 | **无** —— 安装时可能出现 SmartScreen 提示，属正常现象 |
| 与官方包的差异 | 图标自绘；WinSparkle 用仓库自带的 0.8.1（官方 CI 现编 0.9.2 并打补丁禁止更新对话框自动打开浏览器） |

本地构建
--------

```cmd
:: 1) 取预编译 librime（头文件 / 库 / pdb / opencc）
powershell -ExecutionPolicy Bypass -File get-rime.ps1 -use dev

:: 2) 取 Boost 1.90.0 源码并编译（需已装 MSVC，另见 install_boost.bat）
install_boost.bat

:: 3) 在「x64 Native Tools Command Prompt for VS 2022」里执行
copy env.vs2022.bat env.bat
build.bat data        :: 首次需要：用 plum 安装预置输入方案（需联网）
build.bat weasel      :: 编译主体（x64 + Win32）
build.bat installer   :: 打包安装程序 → output\archives\weasel-<版本>-installer.exe
```

> 本分支出现的问题请提到**本仓库** [Issues](https://github.com/zghnby0825/weasel/issues)；
> 上游通用问题仍请走 <https://github.com/rime/weasel/issues>。


【小狼毫】輸入法
================

基於 中州韻輸入法引擎／Rime Input Method Engine 等開源技術

式恕堂 版權所無

[![Download](https://img.shields.io/github/v/release/rime/weasel)](https://github.com/rime/weasel/releases/latest)
[![Build status](https://github.com/rime/weasel/actions/workflows/commit-ci.yml/badge.svg)](https://github.com/rime/weasel/actions/workflows/commit-ci.yml)
[![GitHub Tag](https://img.shields.io/github/tag/rime/weasel.svg)](https://github.com/rime/weasel)

授權條款：GPLv3

項目主頁：https://rime.im

您可能還需要 RIME 用於其他操作系統的發行版：

  * ibus-rime、fcitx5-rime 或 fcitx-rime 用於 Linux
  * 【鼠鬚管】用於 macOS （64位）

安裝輸入法
----------

本品適用於 Windows 8.1 ~ Windows 11

初次安裝時，安裝程序將顯示「安裝選項」對話框。

若要將【小狼毫】註冊到繁體中文（臺灣）鍵盤佈局，請在「輸入語言」欄選擇「中文（臺灣）」，再點擊「安裝」按鈕。

安裝完成後，仍可由開始菜單打開「安裝選項」更改輸入語言。

使用輸入法
----------

選取輸入法指示器菜單裏的【中】字樣圖標，開始用小狼毫寫字。

可通過快捷鍵 <kbd>Ctrl+`</kbd> 或 <kbd>F4</kbd> 呼出方案選單、切換輸入方式。

定製輸入法
----------

通過 開始菜單 » 小狼毫輸入法 訪問設定工具及常用位置。

用戶詞庫、配置文件位於 `%AppData%\Rime`，可通過菜單中的「用戶文件夾」打開。高水平玩家調教 Rime 輸入法常會用到。

修改詞庫、配置文件後，須「重新部署」方可生效。

定製 Rime 的方法，請參考 Wiki [《定製指南》](https://github.com/rime/home/wiki/CustomizationGuide)。如需定製 Weasel 獨有的樣式和行為，請參考本倉庫 [Wiki 頁面](https://github.com/rime/weasel/wiki)。

致謝
----

### 輸入方案設計：

  * 【朙月拼音】系列及【八股文】詞典
    - 部分數據來源於 CC-CEDICT、Android 拼音、新酷音、opencc 等開源項目
    - 維護者：佛振、瑾昀
  * 【注音／地球拼音】
    - 維護者：佛振、瑾昀
  * 【倉頡五代】
    - 發明人：朱邦復先生
    - 碼表源自 www.chinesecj.com
    - 構詞碼表作者：惜緣

  【五笔】【粵拼】【上海／蘇州吳語】【中古漢語拼音】【國際音標】等衆多方案
  不再以安裝包預裝形式提供。可由 <https://github.com/rime/plum> 下載安裝。

### 程序設計：

  * [佛振](https://github.com/lotem)
  * [鄒旭](https://github.com/zouxu09)
  * [Xiangyan Sun](https://github.com/wishstudio)
  * [Prcuvu](https://github.com/Prcuvu)
  * [nameoverflow](https://github.com/nameoverflow)
  * [fxliang](https://github.com/fxliang)
  * [Azuk 443](https://github.com/determ1ne)

  查看更多 [代碼貢獻者](https://github.com/rime/weasel/graphs/contributors)

### 美術：

  * 圖標設計／[Patricivs](https://github.com/Patricivs)
  * 配色方案／Aben、P1461、Patricivs、skoj、佛振、五磅兔

### 本品引用了以下開源軟件：

  * [Boost C++ Libraries](http://www.boost.org/) (Boost Software License)
  * [curl](https://curl.haxx.se/) (MIT/X derivate license)
  * [google-glog](https://github.com/google/glog) (BSD 3-Clause License)
  * [Google Test](https://github.com/google/googletest) (BSD 3-Clause License)
  * [LevelDB](https://github.com/google/leveldb) (BSD 3-Clause License)
  * [librime](https://github.com/rime/librime) (BSD 3-Clause License)
  * [marisa-trie](https://github.com/s-yata/marisa-trie) (BSD 2-Clause License, LGPL 2.1)
  * [OpenCC / 開放中文轉換](https://github.com/BYVoid/OpenCC) (Apache License 2.0)
  * [plum](https://github.com/rime/plum) (GNU Lesser General Public License v3.0)
  * [WinSparkle](https://github.com/vslavik/winsparkle) (MIT License)
  * [yaml-cpp](https://github.com/jbeder/yaml-cpp) (MIT License)
  * [7-Zip](https://www.7-zip.org) (GNU LGPLv2.1+ with unRAR restriction)

問題與反饋
----------

發現程序有 bug，請到 GitHub 反饋
<https://github.com/rime/weasel/issues>

歡迎提交 pull request
<https://github.com/rime/weasel/pulls>

Rime 輸入法（不限於 Windows 平臺）功能、使用方法與配置相關的問題，請反饋到
<https://github.com/rime/home/issues>

聯繫方式
--------

技術交流，歡迎光臨 [Rime 代碼之家](https://github.com/rime/home)，或致信 Rime 開發者 <rimeime@gmail.com>

謝謝！
