# OpenClaw PyAutoGUI Skill

跨平台键鼠自动化控制与图片处理工具

## 简介

本技能提供了一套完整的跨平台自动化工具，支持 Windows、Linux 和 macOS 系统。基于 PyAutoGUI 和 Pillow 实现，可用于：

- 鼠标控制（移动、点击、拖拽、滚动）
- 键盘控制（按键、组合键、文本输入）
- 屏幕操作（截图、获取鼠标位置、获取屏幕尺寸）
- 图片处理（获取图片参数、裁剪图片）

## 快速开始

### 安装依赖

```bash
# 键鼠控制
pip install pyautogui

# 图片处理
pip install Pillow
```

### 基本使用

```bash
# 获取屏幕尺寸
python scripts/keyboard_mouse.py screen_size

# 移动鼠标并点击
python scripts/keyboard_mouse.py mouse_move 500 300
python scripts/keyboard_mouse.py mouse_click left

# 截图
python scripts/keyboard_mouse.py screenshot screenshot.png

# 获取图片信息
python scripts/image_utils.py info screenshot.png
```

## 功能模块

### 1. 键鼠控制 (`keyboard_mouse.py`)

#### 鼠标操作
- `screen_size` - 获取屏幕尺寸
- `mouse_position` - 获取当前鼠标位置
- `mouse_move x y` - 移动鼠标到指定位置
- `mouse_click button` - 点击鼠标（left/right/middle）
- `mouse_click_at x y button` - 在指定位置点击
- `mouse_double_click x y` - 双击
- `mouse_drag x1 y1 x2 y2` - 拖拽
- `mouse_scroll amount` - 滚动（正数向上，负数向下）

#### 键盘操作
- `key_press key` - 按下单个按键
- `key_hotkey key1 key2 ...` - 组合键
- `type_text text` - 输入文字

#### 截图
- `screenshot path` - 截取整个屏幕

### 2. 图片工具 (`image_utils.py`)

#### 获取图片信息
- `info path` - 获取完整信息（尺寸、格式、文件大小等）
- `size path` - 仅获取尺寸（快速模式）

#### 图片处理
- `crop x1 y1 x2 y2` - 裁剪图片

## 示例场景

### 自动发送消息
```bash
# 移动鼠标到输入框，点击，输入文字，发送
python scripts/keyboard_mouse.py mouse_click_at 800 600 left
python scripts/keyboard_mouse.py type_text "Hello World"
python scripts/keyboard_mouse.py key_press enter
```

### 截图并分析
```bash
# 截图并获取图片尺寸
python scripts/keyboard_mouse.py screenshot screen.png
python scripts/image_utils.py info screen.png

# 裁剪出右下角区域
python scripts/image_utils.py crop screen.png 1520 880 1920 1080 -o corner.png
```

### 自动化表单填写
```bash
# 点击第一个输入框
python scripts/keyboard_mouse.py mouse_click_at 500 400 left
python scripts/keyboard_mouse.py type_text "username@example.com"

# 按 Tab 切换到下一个输入框
python scripts/keyboard_mouse.py key_press tab
python scripts/keyboard_mouse.py type_text "password123"

# 点击提交按钮
python scripts/keyboard_mouse.py mouse_click_at 500 600 left
```

## 坐标系统

- **原点 (0, 0)**：屏幕左上角
- **X 轴**：向右增加
- **Y 轴**：向下增加

## 安全提示

1. 操作前确认目标窗口已激活
2. 谨慎使用组合键，避免触发系统快捷键
3. 移动鼠标到屏幕左上角 (0,0) 会触发安全停止
4. 建议在操作前添加延迟，给用户反应时间

## 跨平台支持

| 平台 | 支持状态 | 备注 |
|------|----------|------|
| Windows | ✅ 完全支持 | 可能需要管理员权限 |
| Linux | ✅ 支持 | 需要 X11 环境，Wayland 可能不支持 |
| macOS | ✅ 支持 | 需要在系统设置 > 安全性与隐私 > 辅助功能 中授权 |

## 项目结构

```
openclaw-pyautogui-skill/
├── SKILL.md              # 技能说明文档
├── README.md             # 本文件
└── scripts/
    ├── keyboard_mouse.py # 键鼠控制脚本
    └── image_utils.py    # 图片处理脚本
```

## 依赖

- Python 3.7+
- pyautogui
- Pillow

## 许可证

MIT License
