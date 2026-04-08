# <img src="./assets/ww-logo.png" alt="WhisperWriter icon" width="25" height="25"> WhisperWriter

**WhisperWriter** 是一款轻量级的语音转文字（STT）工具。它利用 OpenAI 的 **Whisper 模型**，能够将你通过麦克风录制的语音自动识别并实时输入到当前处于活动状态的窗口中。

> **💡 有趣的背景：** 本项目的初始版本几乎完全是作者与 **ChatGPT-4** 和 **GitHub Copilot** 结对编程完成的。从代码到这份 README，大部分内容均由 AI 生成。

------

## 🚀 最新更新 (2024-05-28)

项目进行了重大重构！

- **UI 升级：** 界面从 `tkinter` 迁移到了更现代的 `PyQt5`。
- **新增功能：** 增加了独立的设置窗口、**连续录音模式**以及对本地 API 的支持。
- **反馈渠道：** 如果在使用过程中遇到 Bug，欢迎[提交 Issue](https://github.com/savbell/whisper-writer/issues)。

------

## 🛠️ 核心功能

程序在后台运行，通过快捷键（默认 `Ctrl+Shift+Space`）触发录音。

### 1. 四种录音模式

- **`continuous` (连续录音 - 默认)**：检测到说话停顿后自动识别并输入，随后立即开始下一轮录音。再次按下快捷键可停止。
- **`voice_activity_detection` (语音活动检测)**：检测到说话停顿后停止并转录，如需再次录音需手动触发。
- **`press_to_toggle` (点击切换)**：按一下开始，再按一下停止。
- **`hold_to_record` (按住录音)**：按住快捷键时录音，松开即停止并转录。

### 2. 双引擎支持

- **本地运行**：通过 `faster-whisper` 在本地 CPU/GPU 上运行，无需联网，保护隐私。
- **API 模式**：通过 OpenAI 官方 API 或兼容 OpenAI 接口的本地端点（如 LocalAI）进行转录。

------

## 🏁 快速开始

### 1. 环境准备

确保你的系统中已安装：

- **Git**: [下载地址](https://git-scm.com/downloads)
- **Python 3.11**: [下载地址](https://www.python.org/downloads/)

#### **GPU 加速（可选）**

如果你希望使用 NVIDIA 显卡加速本地识别，需要安装：

- [cuBLAS for CUDA 12](https://developer.nvidia.com/cublas)
- [cuDNN 8 for CUDA 12](https://developer.nvidia.com/cudnn)

> **注意**：`faster-whisper` 目前对 CUDA 12 支持较好。Linux 用户可通过 `pip install nvidia-cublas-cu12 nvidia-cudnn-cu12` 快速安装。

### 2. 安装步骤

Bash

```
# 1. 克隆仓库
git clone https://github.com/savbell/whisper-writer
cd whisper-writer

# 2. 创建并激活虚拟环境
python -m venv venv
# Windows:
venv\Scripts\activate
# Linux/macOS:
source venv/bin/activate

# 3. 安装依赖
pip install -r requirements.txt

# 4. 启动程序
python run.py
```

### 3. 初始配置

首次运行会弹出 **Settings（设置）** 窗口。配置完成后点击保存，在主界面点击 **"Start"** 激活监听。

------

## ⚙️ 配置选项说明

### 模型设置 (Model Options)

- `use_api`: 是否使用 OpenAI API（默认为 `false`，即使用本地模型）。
- `language`: 指定识别语言（如 `zh` 代表中文），设为 `null` 则自动检测。
- `local.model`: 本地模型大小（可选 `base`, `small`, `medium`, `large-v3` 等）。模型越大越准，但速度越慢。
- `local.device`: 运行设备。建议显卡用户选 `cuda`，普通用户选 `cpu` 或 `auto`。

### 录音设置 (Recording Options)

- `activation_key`: 触发快捷键（默认 `ctrl+shift+space`）。
- `silence_duration`: 停顿多长时间视为说话结束（毫秒）。

### 后处理 (Post-processing)

- `remove_trailing_period`: 是否移除结尾句号。
- `add_trailing_space`: 转录完成后是否自动加空格。
- `writing_key_press_delay`: 模拟打字输入的速度。

------

## 📝 开发计划 (Roadmap)

- [x] 重构配置结构，减少冗余。
- [x] 支持最新版 OpenAI API。
- [x] UI 界面升级。
- [ ] **新增功能：** 简单的词汇替换（例如：将“笑脸”替换为“😊”）。
- [ ] **新增功能：** 集成 GPT 进行提示词处理（Instructional post-processing）。
- [ ] **打包：** 创建独立的可执行文件（.exe）。

------

## 🤝 贡献与感谢

- **OpenAI**: 感谢 Whisper 模型和 ChatGPT 提供的技术支持。
- **faster-whisper**: 感谢 Guillaume Klein 开发的高效推理库。
- **License**: 本项目采用 **GNU General Public License** 开源协议。

欢迎通过 [Pull Request](https://github.com/savbell/whisper-writer/pulls) 贡献代码或提出改进建议！
