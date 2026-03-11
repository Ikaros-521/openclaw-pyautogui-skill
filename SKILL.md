---
name: openclaw-pyautogui
description: 跨平台键鼠自动化控制技能，支持鼠标控制（移动、点击、拖拽、滚动）、键盘控制（按键、组合键、输入文本）、屏幕操作（截图、获取鼠标位置）、图片处理（获取图片参数、裁剪图片）、屏幕绘图（在屏幕上绘制标记）、图片绘制（在图片上绘制标记）、文件清理（释放磁盘空间）。当用户需要进行自动化键鼠操作、屏幕截图、获取鼠标位置、模拟键盘输入、获取图片信息、裁剪图片、绘制标记或清理文件时激活此技能。
---

# PyAutoGUI 键鼠控制技能

跨平台键鼠自动化控制技能，支持 Windows、Linux、macOS。

## 功能特性

- **鼠标控制**：移动、点击、拖拽、滚动
- **键盘控制**：按键、组合键、输入文本
- **屏幕操作**：截图、获取鼠标位置、获取屏幕尺寸
- **图片处理**：获取图片参数（尺寸、格式、文件大小）、裁剪图片
- **屏幕绘图**：在屏幕上绘制临时标记以确认坐标位置
- **图片绘制**：在图片上永久绘制标记并保存
- **文件清理**：清理截图和标记文件，释放磁盘空间

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
- "在屏幕上绘制标记"
- "在图片上绘制标记"
- "确认坐标位置"
- "标记目标位置"
- "清理文件"
- "删除截图"
- "释放磁盘空间"

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

# Windows 示例
python scripts/keyboard_mouse.py screenshot "E:\\temp\\screenshot.png"
```

**截图参数：**
- 支持格式：PNG（推荐）、JPG、BMP 等
- 截图范围：整个主屏幕（多显示器环境下为主显示器）

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
- `scripts/draw_overlay.py` - 屏幕绘图标记脚本
- `scripts/draw_on_image.py` - 图片绘制标记脚本
- `scripts/cleanup.py` - 文件清理工具脚本

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

### 图片参数说明

| 参数 | 说明 | 示例值 |
|------|------|--------|
| `width` | 图片宽度（像素） | 1920, 3840 |
| `height` | 图片高度（像素） | 1080, 2160 |
| `format` | 图片格式 | PNG, JPEG, GIF, BMP, WEBP |
| `mode` | 颜色模式 | RGB(彩色), RGBA(带透明), L(灰度) |
| `file_size_bytes` | 文件大小（字节） | 2097152 |
| `file_size_kb` | 文件大小（KB） | 2048.0 |

### 坐标系统说明

**屏幕坐标系：**
- 原点 (0, 0) 在屏幕左上角
- X 轴向右增加
- Y 轴向下增加

**裁剪坐标：**
- `x1, y1`: 裁剪区域左上角坐标
- `x2, y2`: 裁剪区域右下角坐标
- 裁剪后的图片尺寸 = (x2 - x1) × (y2 - y1)

**示例：**
```bash
# 从截图中裁剪出右下角的区域 (假设屏幕为 1920x1080)
python3 scripts/image_utils.py crop screenshot.png 1520 880 1920 1080
```

### 图片工具示例场景

#### 分析截图中的元素位置
```bash
# 1. 先获取截图尺寸
python3 scripts/image_utils.py size screenshot.png

# 2. 裁剪出特定区域（如右下角 400x200 区域）
python3 scripts/image_utils.py crop screenshot.png 3440 1960 3840 2160 -o bottom_right.png
```

#### 批量处理图片
```bash
# 快速获取多张图片的尺寸
for img in *.png; do
    echo -n "$img: "
    python3 scripts/image_utils.py size "$img"
done
```

#### 截取屏幕区域
```bash
# 结合截图和裁剪功能获取特定区域
python3 scripts/keyboard_mouse.py screenshot full.png
python3 scripts/image_utils.py crop full.png 500 300 1000 800 -o region.png
```

---

## 屏幕绘图标记

用于在屏幕上绘制临时标记以确认坐标位置，特别适用于：
- 校准坐标位置是否准确
- 确认按钮/元素的实际位置
- 调试自动化脚本

### 绘制标记

```bash
# 在 (500, 300) 绘制十字标记（默认红色，持续 5 秒）
python3 scripts/draw_overlay.py marker cross 500 300

# 绘制靶心标记（圆圈+十字），持续 10 秒
python3 scripts/draw_overlay.py marker target 800 600 --duration 10

# 绘制蓝色圆圈并添加文字标注
python3 scripts/draw_overlay.py marker circle 500 300 --color blue --text "发送按钮"

# 绘制箭头（可指定方向 up/down/left/right）
python3 scripts/draw_overlay.py marker arrow 1000 800 --direction down --color yellow

# 绘制绿色方框
python3 scripts/draw_overlay.py marker square 600 400 --color green --size 40
```

### 绘制区域框选

```bash
# 绘制区域框选，标注 QQ 窗口位置
python3 scripts/draw_overlay.py area 3028 276 3832 2098 --label "QQ窗口" --duration 8

# 标注一个按钮区域
python3 scripts/draw_overlay.py area 3744 2062 3832 2098 --label "发送按钮" --color red
```

### 标记类型说明

| 类型 | 说明 | 用途 |
|------|------|------|
| `cross` | 十字线 | 精确定位单个点 |
| `circle` | 圆圈 | 标记按钮或圆形区域 |
| `square` | 方框 | 标记矩形元素 |
| `arrow` | 箭头 | 指示方向或引导注意 |
| `target` | 靶心 | 最强视觉提示（圆圈+十字） |

### 常用颜色

`red`, `green`, `blue`, `yellow`, `cyan`, `magenta`, `white`, `orange`

### 坐标校准工作流示例

```bash
# 1. 先截图
python3 scripts/keyboard_mouse.py screenshot screen.png

# 2. 分析得到坐标 (3788, 2080)
# 3. 在屏幕上绘制标记验证位置
python3 scripts/draw_overlay.py marker target 3788 2080 --text "发送按钮" --duration 10

# 4. 如果位置不对，调整后重新绘制验证
python3 scripts/draw_overlay.py marker target 3790 2090 --text "发送按钮-修正" --duration 10

# 5. 确认无误后执行点击
python3 scripts/keyboard_mouse.py mouse_click_at 3790 2090 left
```

---

## 图片绘制标记

在图片上永久绘制标记并保存，适用于：
- 在截图上标注识别出的元素位置
- 生成带标注的参考图片
- 批量标记多个位置进行对比
- 保存校准记录

### 绘制标记

```bash
# 在图片上绘制十字标记
python3 scripts/draw_on_image.py screenshot.png marker cross 500 300

# 绘制靶心标记并保存到新文件（不覆盖原图）
python3 scripts/draw_on_image.py screenshot.png marker target 800 600 -o marked.png

# 绘制红色圆圈并添加文字标注
python3 scripts/draw_on_image.py screenshot.png marker circle 500 300 --color red --text "发送按钮"

# 绘制箭头（可指定方向）
python3 scripts/draw_on_image.py screenshot.png marker arrow 1000 800 --direction down --color yellow

# 绘制点标记（小圆点）
python3 scripts/draw_on_image.py screenshot.png marker point 600 400 --color green --size 10
```

### 绘制区域框选

```bash
# 在图片上标注 QQ 窗口区域
python3 scripts/draw_on_image.py screenshot.png area 3028 276 3832 2098 --label "QQ窗口"

# 标注按钮区域并保存为新文件
python3 scripts/draw_on_image.py screenshot.png area 3744 2062 3832 2098 -o button_marked.png --label "发送按钮"
```

### 批量标记工作流

```bash
# 1. 先截图
python3 scripts/keyboard_mouse.py screenshot screen.png

# 2. 标记第一个识别点（不覆盖原图）
python3 scripts/draw_on_image.py screen.png marker target 3788 2080 --text "发送按钮" -o step1.png

# 3. 在 step1.png 上标记修正位置
python3 scripts/draw_on_image.py step1.png marker target 3790 2090 --text "修正位置" -o step2.png

# 4. 继续添加更多标记...
python3 scripts/draw_on_image.py step2.png marker circle 3000 1500 --text "头像区域" -o final.png
```

### 屏幕绘图 vs 图片绘制对比

| 对比项 | 屏幕绘图 (draw_overlay.py) | 图片绘制 (draw_on_image.py) |
|--------|---------------------------|---------------------------|
| **显示位置** | 屏幕上实时显示 | 在图片文件中 |
| **持续时间** | 临时（几秒后自动关闭） | 永久保存 |
| **交互方式** | 点击或按键关闭 | 无需交互 |
| **适用场景** | 实时校准坐标 | 生成标注参考图 |
| **保存结果** | 不保存 | 保存为新图片 |
| **费用** | 实时验证，较费钱 | 批量处理，较省钱 |

### 推荐的坐标校准流程（省钱版）

```bash
# 1. 截图
python3 scripts/keyboard_mouse.py screenshot screen.png

# 2. 获取图片尺寸
python3 scripts/image_utils.py size screen.png

# 3. 分析并标记到图片上（批量标记多个可能位置，省钱！）
python3 scripts/draw_on_image.py screen.png marker target 3788 2080 --text "候选1" -o marked1.png
python3 scripts/draw_on_image.py screen.png marker target 3790 2090 --text "候选2" -o marked2.png
python3 scripts/draw_on_image.py screen.png marker target 3785 2085 --text "候选3" -o marked3.png

# 4. 查看标记后的图片，选择最准确的位置
# 5. 最后只在确定正确的位置执行一次屏幕绘图确认
python3 scripts/draw_overlay.py marker target 3790 2090 --duration 3

# 6. 确认无误后执行点击
python3 scripts/keyboard_mouse.py mouse_click_at 3790 2090 left
```

---

## 文件清理工具

用于清理截图和标记过程中产生的临时文件，释放磁盘空间。

### 分析文件占用

```bash
# 分析当前目录的临时文件
python3 scripts/cleanup.py analyze .

# 查看文件列表和占用空间
```

### 清理文件

```bash
# 预览清理（超过7天的文件，不实际删除）
python3 scripts/cleanup.py clean . --days 7

# 真正执行清理
python3 scripts/cleanup.py clean . --days 7 --execute

# 清理大于1MB的文件
python3 scripts/cleanup.py clean . --size 1024 --execute

# 清理所有临时文件（谨慎使用！）
python3 scripts/cleanup.py clean . --execute
```

### 自动清理

```bash
# 自动保持最多50个文件或100MB空间
python3 scripts/cleanup.py auto . --max-files 50 --max-size 100

# 自定义限制
python3 scripts/cleanup.py auto . --max-files 20 --max-size 50
```

### 完整工作流程示例

```bash
# 1. 截图并标记
python3 scripts/keyboard_mouse.py screenshot screen.png
python3 scripts/draw_on_image.py marker screen.png target 500 300 --text "按钮" -o marked.png

# 2. 分析文件占用
python3 scripts/cleanup.py analyze .

# 3. 确认后清理旧文件
python3 scripts/cleanup.py clean . --days 1 --execute

# 或者设置自动清理
python3 scripts/cleanup.py auto . --max-files 10 --max-size 50
```

---

## 命令速查表

### 键鼠控制脚本

| 命令 | 功能 | 示例 |
|------|------|------|
| `screen_size` | 获取屏幕尺寸 | `keyboard_mouse.py screen_size` |
| `mouse_position` | 获取鼠标位置 | `keyboard_mouse.py mouse_position` |
| `mouse_move x y` | 移动鼠标 | `keyboard_mouse.py mouse_move 500 300` |
| `mouse_click button` | 点击鼠标 | `keyboard_mouse.py mouse_click left` |
| `mouse_click_at x y button` | 指定位置点击 | `keyboard_mouse.py mouse_click_at 500 300 left` |
| `mouse_double_click x y` | 双击 | `keyboard_mouse.py mouse_double_click 500 300` |
| `mouse_drag x1 y1 x2 y2` | 拖拽 | `keyboard_mouse.py mouse_drag 500 300 800 600` |
| `mouse_scroll amount` | 滚动 | `keyboard_mouse.py mouse_scroll 5` |
| `key_press key` | 按键 | `keyboard_mouse.py key_press enter` |
| `key_hotkey key1 key2` | 组合键 | `keyboard_mouse.py key_hotkey ctrl c` |
| `type_text text` | 输入文字 | `keyboard_mouse.py type_text "Hello"` |
| `screenshot path` | 截图 | `keyboard_mouse.py screenshot img.png` |

### 图片工具脚本

| 命令 | 功能 | 示例 |
|------|------|------|
| `info path` | 获取完整信息 | `image_utils.py info photo.png` |
| `size path` | 仅获取尺寸 | `image_utils.py size photo.jpg` |
| `crop x1 y1 x2 y2` | 裁剪图片 | `image_utils.py crop img.png 100 100 500 500` |

### 屏幕绘图脚本

| 命令 | 功能 | 示例 |
|------|------|------|
| `marker type x y` | 绘制标记 | `draw_overlay.py marker target 500 300` |
| `area x1 y1 x2 y2` | 绘制区域框 | `draw_overlay.py area 100 100 500 400` |

### 图片绘制脚本

| 命令 | 功能 | 示例 |
|------|------|------|
| `marker type x y` | 绘制标记到图片 | `draw_on_image.py img.png marker target 500 300` |
| `area x1 y1 x2 y2` | 绘制区域框到图片 | `draw_on_image.py img.png area 100 100 500 400` |

### 文件清理脚本

| 命令 | 功能 | 示例 |
|------|------|------|
| `analyze dir` | 分析文件占用 | `cleanup.py analyze .` |
| `clean dir` | 清理文件 | `cleanup.py clean . --days 7 --execute` |
| `auto dir` | 自动清理 | `cleanup.py auto . --max-files 50` |
