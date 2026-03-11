---
name: openclaw-pyautogui
description: 跨平台键鼠自动化控制技能，支持鼠标控制（移动、点击、拖拽、滚动）、键盘控制（按键、组合键、输入文本）、屏幕操作（截图、获取鼠标位置）、图片处理（获取图片参数、裁剪图片）。当用户需要进行自动化键鼠操作、屏幕截图、获取鼠标位置、模拟键盘输入、获取图片尺寸/格式信息或裁剪图片时激活此技能。
---

# PyAutoGUI 键鼠控制技能

跨平台键鼠自动化控制技能，支持 Windows、Linux、macOS。

## 功能特性

- **鼠标控制**：移动、点击、拖拽、滚动
- **键盘控制**：按键、组合键、输入文本
- **屏幕操作**：截图、获取鼠标位置、获取屏幕尺寸
- **图片处理**：获取图片参数（尺寸、格式、文件大小）、裁剪图片

## 触发条件

当用户需要进行以下操作时激活：
- "点击屏幕上的某个位置"
- "移动鼠标到指定坐标"
- "输入文字/按键"
- "截图"
- "自动执行重复操作"
- "模拟键盘鼠标"
- "获取鼠标位置"
- "获取图片尺寸/参数"
- "查看图片信息"
- "裁剪图片"

## 使用方法

### 安装依赖

```bash
# 键鼠控制依赖
pip3 install pyautogui

# 图片处理依赖
pip3 install Pillow
```

### 获取屏幕信息

```bash
# 获取屏幕尺寸
python3 scripts/keyboard_mouse.py screen_size

# 获取当前鼠标位置
python3 scripts/keyboard_mouse.py mouse_position
```

### 鼠标操作

```bash
# 移动鼠标到指定位置 (x, y)
python3 scripts/keyboard_mouse.py mouse_move 500 300
python3 scripts/keyboard_mouse.py mouse_move 500 300 --duration 1.0

# 点击鼠标（左键/右键/中键）
python3 scripts/keyboard_mouse.py mouse_click left
python3 scripts/keyboard_mouse.py mouse_click right
python3 scripts/keyboard_mouse.py mouse_click middle --clicks 2

# 在指定位置点击
python3 scripts/keyboard_mouse.py mouse_click_at 500 300 left
python3 scripts/keyboard_mouse.py mouse_click_at 500 300 right --clicks 2

# 双击
python3 scripts/keyboard_mouse.py mouse_double_click 500 300

# 拖拽
python3 scripts/keyboard_mouse.py mouse_drag 500 300 800 600
python3 scripts/keyboard_mouse.py mouse_drag 500 300 800 600 --duration 2.0

# 滚动（正数向上，负数向下）
python3 scripts/keyboard_mouse.py mouse_scroll 5
python3 scripts/keyboard_mouse.py mouse_scroll -3
```

### 键盘操作

```bash
# 按单个键
python3 scripts/keyboard_mouse.py key_press enter
python3 scripts/keyboard_mouse.py key_press escape
python3 scripts/keyboard_mouse.py key_press tab
python3 scripts/keyboard_mouse.py key_press space

# 组合键
python3 scripts/keyboard_mouse.py key_hotkey ctrl c
python3 scripts/keyboard_mouse.py key_hotkey ctrl v
python3 scripts/keyboard_mouse.py key_hotkey win r
python3 scripts/keyboard_mouse.py key_hotkey alt tab
python3 scripts/keyboard_mouse.py key_hotkey ctrl alt t

# 输入文字
python3 scripts/keyboard_mouse.py type_text "Hello World"
python3 scripts/keyboard_mouse.py type_text "你好世界" --interval 0.05
```

### 截图

```bash
# 截取整个屏幕
python3 scripts/keyboard_mouse.py screenshot /tmp/screenshot.png
```

## 常用按键名称

- 字母：`a` `b` `c` ...
- 数字：`0` `1` `2` ...
- 功能键：`f1` `f2` ... `f12`
- 控制键：`ctrl` `alt` `shift` `win`
- 其他：`enter` `esc` `tab` `space` `backspace` `delete` `up` `down` `left` `right`

## 安全提示

⚠️ **重要**：使用此技能时请确保：
1. 操作前确认目标窗口已激活
2. 谨慎使用组合键，避免触发系统快捷键
3. 建议在操作前添加延迟，给用户反应时间
4. 移动鼠标到屏幕左上角 (0,0) 会触发安全停止

## 跨平台注意事项

- **Windows**: 完全支持所有功能，可能需要管理员权限
- **Linux**: 需要 X11 环境，Wayland 可能不支持
- **macOS**: 需要在 系统设置 > 安全性与隐私 > 辅助功能 中授权终端或 Python

## 示例场景

### 打开计算器并计算
```bash
# Windows 打开计算器
python3 scripts/keyboard_mouse.py key_hotkey win r
python3 scripts/keyboard_mouse.py type_text "calc"
python3 scripts/keyboard_mouse.py key_press enter
```

### 自动填写表单
```bash
# 移动并点击输入框
python3 scripts/keyboard_mouse.py mouse_click_at 500 300 left
# 输入内容
python3 scripts/keyboard_mouse.py type_text "example@email.com"
# 按Tab跳到下一个输入框
python3 scripts/keyboard_mouse.py key_press tab
# 输入密码
python3 scripts/keyboard_mouse.py type_text "password123"
```

### 批量点击
```bash
# 在多个位置连续点击
python3 scripts/keyboard_mouse.py mouse_click_at 100 100 left
python3 scripts/keyboard_mouse.py mouse_click_at 200 200 left
python3 scripts/keyboard_mouse.py mouse_click_at 300 300 left
```

## 依赖文件

- `scripts/keyboard_mouse.py` - 主控制脚本
- `scripts/image_utils.py` - 图片工具脚本

## 图片工具

### 获取图片信息

```bash
# 获取图片完整信息（尺寸、格式、文件大小等）
python3 scripts/image_utils.py info screenshot.png

# 仅获取图片尺寸（快速模式）
python3 scripts/image_utils.py size photo.jpg
```

### 裁剪图片

```bash
# 裁剪指定区域 (x1, y1, x2, y2)
python3 scripts/image_utils.py crop screenshot.png 100 100 500 500

# 裁剪并指定输出路径
python3 scripts/image_utils.py crop screenshot.png 100 100 500 500 -o output.png
```

### 输出示例

```bash
$ python3 scripts/image_utils.py info screenshot.png
{
  "path": "screenshot.png",
  "filename": "screenshot.png",
  "size": {
    "width": 3840,
    "height": 2160
  },
  "format": "PNG",
  "mode": "RGB",
  "file_size_bytes": 2097152,
  "file_size_kb": 2048.0
}
```
