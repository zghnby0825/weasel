【小狼毫】自用分支
==================

基於 **中州韻輸入法引擎（Rime Input Method Engine）** 等開源技術的 Windows 輸入法。

本倉庫是【小狼毫】的**自用分支**：引擎、方案與行為與上游一致，只換掉了狀態圖標，並提供自用的自動構建與安裝包。

* 下載：本倉庫 [Releases](https://github.com/zghnby0825/weasel/releases)（預發布，不定期更新）
* 授權條款：[GPLv3](https://github.com/zghnby0825/weasel/blob/pb/LICENSE.txt)
* 上游倉庫：[fxliang/weasel](https://github.com/fxliang/weasel)（項目主頁 <https://rime.im>）

本分支說明（自用）
------------------

在上游代碼基礎上只做了兩件事：

### 1. 重繪狀態圖標

英文 `英`、中文 `中`、全角 `全`、半角 `半`、部署中 `↻`、程序圖標 —— 六個圖標全部重繪：

![狀態圖標概覽](https://raw.githubusercontent.com/zghnby0825/weasel/pb/docs/icons/overview.png)

| 圖標 | 文件 | 資源 ID | 用途 |
| :--: | :-- | :-- | :-- |
| <img src="https://raw.githubusercontent.com/zghnby0825/weasel/pb/docs/icons/en.png" width="32" alt="英"> | `resource/en.ico` | `IDI_EN` | 英文（ASCII）模式 |
| <img src="https://raw.githubusercontent.com/zghnby0825/weasel/pb/docs/icons/zh.png" width="32" alt="中"> | `resource/zh.ico` | `IDI_ZH` | 中文模式 |
| <img src="https://raw.githubusercontent.com/zghnby0825/weasel/pb/docs/icons/full.png" width="32" alt="全"> | `resource/full.ico` | `IDI_FULL_SHAPE` | 全角 |
| <img src="https://raw.githubusercontent.com/zghnby0825/weasel/pb/docs/icons/half.png" width="32" alt="半"> | `resource/half.ico` | `IDI_HALF_SHAPE` | 半角 |
| <img src="https://raw.githubusercontent.com/zghnby0825/weasel/pb/docs/icons/reload.png" width="32" alt="↻"> | `resource/reload.ico` | `IDI_RELOAD` | 部署中 |
| <img src="https://raw.githubusercontent.com/zghnby0825/weasel/pb/docs/icons/weasel.png" width="32" alt="程序圖標"> | `resource/weasel.ico` | `IDI_ICON` | 程序 / 窗口圖標 |

* **無框 · 白色字形 + 深灰描邊 · 透明底**，深色任務欄與淺色任務欄下都看得清（描邊寬約為筆畫的 0.045 倍）
* 字形取自 [Maple Mono NF CN](https://github.com/subframe7536/maple-font) 的位圖渲染，`↻` 為幾何手繪（同字體無此字形）
* 程序圖標去掉原版的黑色圓角底，只留白色字形，與其餘五個統一為同一套風格
* **字形連同描邊整體等比縮放到填滿畫布**，不預留邊距，確保任務欄 16px 下最大可讀
* 源碼即 `resource/*.ico`，每個文件六個尺寸檔位：16 / 24 / 32 / 48 / 64（32bpp DIB）+ 256（PNG 壓縮）
* 上表預覽圖由 `resource/*.ico` 的 256 檔等比縮出，存於 `docs/icons/`
* 改完 `.ico` 必須 `build.bat rebuild` —— 資源腳本不把 `.ico` 當作輸入依賴，增量編譯不會重新嵌圖標

### 2. 自用自動構建

推一個**數字開頭**的 tag（如 `0.17.4-personal-20261005`）即觸發 CI，編譯後直接發布 Release 附安裝包，見下節。

![Personal Build](https://img.shields.io/github/v/release/zghnby0825/weasel?include_prereleases&label=personal%20build)

自用構建（Personal Build）
--------------------------

| 項目 | 說明 |
| :-- | :-- |
| 發布頁 | <https://github.com/zghnby0825/weasel/releases> |
| 版本號 | `0.17.4`（取自 `weasel.props` 的 `PRODUCT_VERSION`） |
| 架構 | **x64 + x86 + ARM64 + ARM64X**（安裝包會按系統自動選擇） |
| 構建環境 | Visual Studio 2022 生成工具 17.14 / MSVC 14.44（v143）/ Windows SDK 10.0.26100（CI 用 10.0.19041）/ Boost 1.90.0 / librime 1.17.0 / NSIS 3.12 |
| 代碼簽名 | **無** —— 安裝時可能出現 SmartScreen 提示，屬正常現象 |
| 觸發方式 | 推 tag（`[0-9]+.*`）或 Actions 頁面手動 `Run workflow` |
| 附帶產物 | 安裝包 `weasel-<版本>-installer.exe` + 調試符號 `debug_symbols.7z` |

安裝輸入法
----------

本品適用於 Windows 8.1 ~ Windows 11。

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

修改詞庫、配置文件後，須「重新部署」方可生效。定製輸入法的方法，請參考 Wiki [《定製指南》](https://github.com/rime/home/wiki/CustomizationGuide)；
小狼毫獨有的樣式與行為選項，見安裝目錄下 `weasel.yaml` 內的註釋與示例。

本地構建
--------

```cmd
:: 1) 取預編譯 librime（頭文件 / 庫 / pdb / opencc）
powershell -ExecutionPolicy Bypass -File get-rime.ps1 -use dev

:: 2) 取 Boost 1.90.0 源碼並編譯（需已裝 MSVC，見 install_boost.bat）
install_boost.bat

:: 3) 在「x64 Native Tools Command Prompt for VS 2022」裏執行
copy env.vs2022.bat env.bat
build.bat data        :: 首次需要：用 plum 安裝預置輸入方案（需聯網）
build.bat weasel      :: 編譯主體（x64 + Win32）
build.bat arm64       :: 追加 ARM64 / ARM64X（需裝對應工具集，見注 2）
build.bat installer   :: 打包安裝程序 → output\archives\weasel-<版本>-installer.exe
```

> 注 1：`get-rime.ps1 -use` 結束時會停掉正在運行的小狼毫服務，僅影響本機正在使用的輸入法。
> 注 2：ARM64 需要 VS 2022 的 `VC.Tools.ARM64` / `VC.Tools.ARM64EC` / `VC.Tools.ARM` 組件
> 與 Windows SDK 10.0.19041（ARM32 目標），CI 的 `windows-2022` 已預裝。
> 注 3：`build.bat` 編譯前會調用 `output\weaselserver.exe /q` 退出服務，編譯完記得重新啟動。

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

### 美術：

  * 原版圖標設計／[Patricivs](https://github.com/Patricivs)
  * 配色方案／Aben、P1461、Patricivs、skoj、佛振、五磅兔
  * 本分支狀態圖標／自繪，字形取自 [Maple Mono NF CN](https://github.com/subframe7536/maple-font)

### 本品引用了以下開源軟件：

  * [Boost C++ Libraries](http://www.boost.org/) (Boost Software License)
  * [curl](https://curl.haxx.se/) (MIT/X derivate license)
  * [google-glog](https://github.com/google/glog) (BSD 3-Clause License)
  * [Google Test](https://github.com/google/googletest) (BSD 3-Clause License)
  * [LevelDB](https://github.com/google/leveldb) (BSD 3-Clause License)
  * [librime](https://github.com/rime/librime) (BSD 3-Clause License)
  * [Maple Mono](https://github.com/subframe7536/maple-font) (SIL Open Font License 1.1，本分支圖標字形來源)
  * [marisa-trie](https://github.com/s-yata/marisa-trie) (BSD 2-Clause License, LGPL 2.1)
  * [OpenCC / 開放中文轉換](https://github.com/BYVoid/OpenCC) (Apache License 2.0)
  * [plum](https://github.com/rime/plum) (GNU Lesser General Public License v3.0)
  * [WinSparkle](https://github.com/vslavik/winsparkle) (MIT License)
  * [yaml-cpp](https://github.com/jbeder/yaml-cpp) (MIT License)
  * [7-Zip](https://www.7-zip.org) (GNU LGPLv2.1+ with unRAR restriction)

問題與反饋
----------

本分支出現的問題，請提到本倉庫 [Issues](https://github.com/zghnby0825/weasel/issues)。

引擎、方案、配置等與本分支改動無關的通用問題，請反饋到
<https://github.com/fxliang/weasel/issues>。
