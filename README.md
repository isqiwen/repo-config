# repo-config

用于提供一套面向 `C++20` 项目的仓库根目录配置基线，统一 Git、编辑器和代码格式化行为。适合使用 `CMake`、`Ninja`、`Visual Studio` 的工程，也兼顾仓库中的 Python、shell、PowerShell 辅助脚本。

## 适用场景

- C++20 项目
- 使用 CMake 作为主要构建系统
- 常见开发环境包含 Ninja 或 Visual Studio
- 仓库中包含少量 Python、shell、PowerShell 脚本
- 希望统一 UTF-8、LF、缩进和 C++ 格式化风格

## 包含内容

| 文件 | 说明 | 主要约定 |
| --- | --- | --- |
| `.gitignore` | 忽略常见构建产物、缓存和临时文件 | 覆盖 CMake、Ninja、Visual Studio 生成物，忽略 Python 缓存，并忽略仓库根目录的 `/Makefile` |
| `.editorconfig` | 统一编辑器基础行为 | 默认 UTF-8、LF、末尾换行、2 空格缩进；Python 使用 4 空格；shell / PowerShell / Batch 使用 2 空格；`Makefile` 使用 tab |
| `.clang-format` | 统一 C/C++ 代码格式 | 基于 LLVM 风格，2 空格缩进，120 列限制，语言标准固定为 `Cpp20` |
| `.gitattributes` | 统一 Git 对文本和二进制文件的处理方式 | 文本文件统一使用 `LF`，`.bat` / `.cmd` 显式使用 `CRLF`，常见二进制资源显式标记为 `binary` |

## 默认约定

- 文本文件默认使用 `UTF-8` 和 `LF`
- 所有文件默认保留末尾换行
- C/C++ 代码使用 2 空格缩进，并按 `Cpp20` 进行格式化
- Python 使用 4 空格缩进
- shell 和 PowerShell 脚本使用 2 空格缩进
- Batch 脚本使用 2 空格缩进，并保持 `CRLF`
- `Makefile` 保持 tab 缩进
- 推荐使用 out-of-source build，避免在源码目录混入构建产物

## 使用方式

将这些文件放在仓库根目录即可生效。对于新项目，可以直接作为初始配置使用；对于已有项目，建议在引入后统一做一次格式化和行尾整理，减少后续噪音提交。

如果项目有特殊约定，可以按需调整：

- 需要提交手写的 Visual Studio 工程文件时，修改 `.gitignore` 中与 `*.sln`、`*.vcxproj` 相关的规则
- 需要在其他目录保留手写 `Makefile` 时，保留当前 `/Makefile` 规则即可；如果连根目录 `Makefile` 也需要跟踪，再移除该规则
- 如果仓库增加更多脚本类型或配置格式，可继续扩展 `.editorconfig` 和 `.gitattributes`

## 脚本说明

这套配置已经为 shell、PowerShell、Batch 脚本统一了编码、行尾和缩进，但它本身不替代专门的脚本格式化工具。若脚本数量较多，推荐搭配以下工具使用：

- shell：`shfmt`、`shellcheck`
- PowerShell：`PSScriptAnalyzer`、`Invoke-Formatter`

## 维护原则

- 只为仓库中真实使用的语言和工具链添加规则
- 优先保持规则清晰、稳定、易维护
- 避免为了假想场景提前堆积过多配置
