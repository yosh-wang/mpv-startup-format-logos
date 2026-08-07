
---

## ⚙️ 配置说明

配置文件 `script-opts/startup_format_logos.conf` 中的完整选项：

### 基础选项

| 选项 | 默认值 | 说明 |
|------|--------|------|
| `enabled` | `yes` | 是否启用 |
| `style` | `color` | `color` = 彩色徽章，`white` = 透明白色图标 |
| `show_video` | `yes` | 是否显示画面标准 Logo |
| `show_audio` | `yes` | 是否显示音频标准 Logo |
| `show_sdr` | `yes` | 是否为普通 SDR 画面显示彩色 SDR 徽章 |
| `show_common_audio` | `yes` | 是否显示 FLAC、PCM、AAC、Opus、MP3 等常见音频格式徽章 |
| `require_video` | `no` | 是否只在存在真实视频轨时显示 |
| `filename_fallback` | `yes` | 是否允许从文件名/媒体标题/路径补充识别 |
| `show_on_audio_change` | `yes` | 切换音轨后是否短暂显示新的音频格式 Logo |

### 位置与布局

| 选项 | 默认值 | 说明 |
|------|--------|------|
| `position` | `top-right` | 位置：`top-right`、`top-left`、`bottom-right`、`bottom-left` |
| `anchor_to_video` | `yes` | 是否以实际视频画面边界为定位基准 |
| `detect_encoded_bars` | `yes` | 是否检测编码进视频帧的黑边（常见于蓝光 ISO） |
| `encoded_bar_threshold` | `16` | 黑边 RGB 阈值（0-48），越高越容易识别较浅的黑边 |
| `encoded_bar_delay` | `0.18` | 等待画面稳定后抽样编码黑边的时间（秒） |
| `margin_x` | `60` | 水平安全边距（随分辨率自动缩放） |
| `margin_y` | `38` | 垂直安全边距（随分辨率自动缩放） |

### 缩放与尺寸

| 选项 | 默认值 | 说明 |
|------|--------|------|
| `scale` | `1.0` | 整体缩放倍率 |
| `portrait_scale` | `1.18` | 竖屏模式下徽章额外倍率 |

### 时间控制

| 选项 | 默认值 | 说明 |
|------|--------|------|
| `delay` | `0.45` | 等待画面就绪后延迟显示的时间（秒） |
| `hold` | `4.0` | 完全显示后的停留时间（秒） |
| `fade_in` | `0.12` | 淡入时间（秒），设为 `0` 关闭 |
| `fade_out` | `0.18` | 淡出时间（秒），设为 `0` 关闭 |
| `frame_wait_timeout` | `5.0` | 等待首帧的最长时间（秒） |

### 重试与优先级

| 选项 | 默认值 | 说明 |
|------|--------|------|
| `retry_interval` | `0.25` | 轨道信息未就绪时的重试间隔（秒） |
| `retry_count` | `8` | 最大检测次数 |
| `video_priority` | `dolby-vision,hdr-vivid,hdr10-plus,hdr10,hlg,sdr` | 视频格式优先级 |
| `audio_priority` | `dolby-atmos,dts-x,audio-vivid,...` | 音频格式优先级 |

### 高级选项

| 选项 | 默认值 | 说明 |
|------|--------|------|
| `asset_dir` | `~~/script-assets/startup-format-logos/runtime` | 资源目录 |
| `overlay_id` | `50` | 占用的 overlay ID（连续三个，默认 50、51、52） |

---

## 📨 脚本消息

可通过 `mp.commandv("script-message", ...)` 调用：

| 消息 | 参数 | 说明 |
|------|------|------|
| `startup-format-logos-show` | 无 | 手动触发检测并显示 |
| `startup-format-logos-preview` | `<video_slug>` `<audio_slug>` | 预览指定格式组合 |
| `startup-format-logos-hide` | 无 | 隐藏 Logo |
| `startup-format-logos-toggle` | 无 | 开关启用状态 |
| `startup-format-logos-set-style` | `color` / `white` | 切换样式 |

### 使用示例

```lua
-- 在 mpv 中通过脚本调用
mp.commandv("script-message", "startup-format-logos-toggle")

-- 预览 Dolby Vision + Dolby Atmos
mp.commandv("script-message", "startup-format-logos-preview", "dolby-vision", "dolby-atmos")
