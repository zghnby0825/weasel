# Building Weasel (this fork)

本分支的構建步驟以 [README](README.md) 的「本地構建」一節為準，一份簡版：

```cmd
:: 1) 取預編譯 librime（頭文件 / 庫 / pdb / opencc）
powershell -ExecutionPolicy Bypass -File get-rime.ps1 -use dev

:: 2) 取 Boost 1.90.0 並編譯
install_boost.bat

:: 3) 在「x64 Native Tools Command Prompt for VS 2022」裏
copy env.vs2022.bat env.bat
build.bat data        :: 首次：用 plum 安裝預置方案（需聯網）
build.bat weasel      :: 主體（x64 + Win32）
build.bat arm64       :: 追加 ARM64 / ARM64X（需對應工具集）
build.bat installer   :: 安裝程序 → output\archives\weasel-<版本>-installer.exe
```

* `BOOST_ROOT` 需指向 Boost 目錄；`env.vs2022.bat` 已按 VS 2022 / v143 / SDK 10.0.26100 配好，需要別的工具集時自行改。
* 已有現成 librime 二進制時，把 `.dll` 放進 `output\`、`.lib` 放進 `lib\`，再 `build.bat weasel` 即可。
* 改過 `resource\*.ico` 要 `build.bat rebuild`，否則增量編譯不會重新嵌圖標。
