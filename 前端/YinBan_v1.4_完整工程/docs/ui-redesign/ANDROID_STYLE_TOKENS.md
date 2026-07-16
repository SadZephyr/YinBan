# YinBan Android Style Tokens

本文件定义唯一、可直接映射到 Android XML 的 UI Token 体系。阶段 6 实施不得创建第二套主题，不得自行调整 HEX，不得新增未经定义的强调色。

## 1. 颜色 Token

| Android Token | HEX | 用途 | 禁止用途 | 对应状态 |
| --- | --- | --- | --- | --- |
| `yb_color_primary` | `#5B5CEB` | 主按钮、选中态、底部导航选中项、重点交互 | 大面积背景、长期状态栏、危险态 | 重点交互 |
| `yb_color_primary_pressed` | `#4949D8` | 主按钮按压态，只由 `#5B5CEB` 加深生成 | 新品牌色、渐变、状态色 | 按压 |
| `yb_color_primary_container` | `#EEF0FF` | 选中背景、弱强调、品牌浅底 | 页面大面积铺底、危险态 | 弱强调 |
| `yb_color_background` | `#F7F7FC` | 页面背景 | 按钮实心色、危险态 | 默认背景 |
| `yb_color_surface` | `#FFFFFF` | 主卡片、弹窗、输入面 | 高风险状态底色 | 默认表面 |
| `yb_color_surface_variant` | `#F1F2FA` | 输入框、空态容器、禁用底 | 主按钮、危险按钮 | 次级表面 |
| `yb_color_text_primary` | `#101426` | 标题、正文、核心数据 | 禁用文字、分割线 | 主要文本 |
| `yb_color_text_secondary` | `#73758A` | 辅助说明、次级状态 | 主标题、危险状态 | 次级文本 |
| `yb_color_border` | `#E2E5F2` | 卡片描边、输入框描边、分割线 | 状态表达主色 | 边界 |
| `yb_color_status_connected` | `#20A66A` | 在线、已连接、可用 | 普通品牌强调、等待态 | 已连接 |
| `yb_color_status_waiting` | `#D98200` | 等待患者、等待连接、处理中 | 危险态、主按钮 | 等待 |
| `yb_color_status_offline` | `#8A8FA3` | 离线、断开、禁用、不可用 | 已连接、SOS | 离线 |
| `yb_color_status_warning` | `#F2A51A` | 温和提醒、注意 | 主品牌、长期大面积背景 | 注意 |
| `yb_color_status_danger` | `#D92D2D` | SOS、危险确认、高风险 | 普通错误以外的装饰、普通按钮 | 危险 |
| `yb_color_overlay` | `#66000000` | 弹窗遮罩、模态背景 | 页面常驻背景 | 遮罩 |

`yb_color_primary_pressed` 只用于按钮按压态，不得发展出新的品牌主题。

## 2. 间距 Token

| Token | 值 | 用途 |
| --- | --- | --- |
| `yb_spacing_4` | 4dp | 小型文本与图标间距 |
| `yb_spacing_8` | 8dp | 标签内距、小控件间距 |
| `yb_spacing_12` | 12dp | 卡片内部紧凑间距 |
| `yb_spacing_16` | 16dp | 控件组间距、卡片间距 |
| `yb_spacing_20` | 20dp | 页面水平边距、卡片内边距 |
| `yb_spacing_24` | 24dp | 页面主区块间距 |
| `yb_spacing_32` | 32dp | 登录页品牌区与表单区间距 |
| `yb_spacing_page_horizontal` | 20dp | 页面左右边距 |
| `yb_spacing_card_padding` | 20dp | 主卡片内边距 |

## 3. 圆角 Token

| Token | 值 | 用途 |
| --- | --- | --- |
| `yb_radius_small` | 8dp | 状态标签、小型底色 |
| `yb_radius_medium` | 14dp | 输入框、按钮 |
| `yb_radius_large` | 18dp | 信息卡、功能入口卡 |
| `yb_radius_dialog` | 16dp | SOS 确认、普通弹窗 |
| `yb_radius_video` | 18dp | 视频占位容器 |
| `yb_radius_video_container` | 18dp | 监护人视频卡片与通话视频容器外层 |

## 4. 尺寸 Token

| Token | 值 | 用途 |
| --- | --- | --- |
| `yb_size_button_height` | 54dp | 主按钮高度 |
| `yb_size_input_height` | 56dp | 输入框高度 |
| `yb_size_bottom_nav_height` | 72dp | 底部导航高度 |
| `yb_size_icon` | 24dp | 正式功能图标基准 |
| `yb_size_entry_icon` | 28dp | 入口卡图标 |
| `yb_size_avatar` | 64dp | 用户头像 |
| `yb_size_logo_normal` | 32dp-64dp | 普通页面小影火 Logo |
| `yb_size_logo_hero` | 96dp | 登录页或 AI 主视觉 Logo 上限 |
| `yb_size_status_label_height` | 28dp | 状态标签高度 |
| `yb_size_call_control` | 64dp | 通话控制按钮 |
| `yb_size_sos_button_height` | 56dp | SOS 主控件高度 |
| `yb_size_touch_target_min` | 48dp | 最小可触达尺寸 |
| `yb_size_video_min_height` | 360dp | 监护人首页视频区域最小高度，避免退化为缩略图 |

## 5. 字体 Token

| Token | sp | 字重 | 建议行高 | 使用场景 |
| --- | --- | --- | --- | --- |
| `yb_text_display` | 32sp | Semibold | 40sp | 登录品牌标题、少量大标题 |
| `yb_text_page_title` | 28sp | Semibold | 34sp | 页面主标题 |
| `yb_text_section_title` | 20sp | Semibold | 26sp | 分区标题、卡片标题 |
| `yb_text_body` | 16sp | Regular | 24sp | 正文、输入内容 |
| `yb_text_body_secondary` | 14sp | Regular | 20sp | 辅助说明、次级文本 |
| `yb_text_status` | 13sp | Medium | 18sp | 状态标签、连接说明 |
| `yb_text_button` | 17sp | Semibold | 22sp | 主按钮、重要操作按钮 |
| `yb_text_data` | 26sp | Bold | 32sp | 实时数据、核心数值 |

## 6. Drawable 命名建议

| 名称 | 用途 |
| --- | --- |
| `yb_bg_page` | 页面背景 |
| `yb_bg_card` | 普通卡片 |
| `yb_bg_card_selected` | 选中卡片 |
| `yb_bg_input` | 输入框背景 |
| `yb_bg_button_primary` | 主按钮 |
| `yb_bg_button_secondary` | 次按钮 |
| `yb_bg_button_danger` | 危险按钮 |
| `yb_bg_status_connected` | 已连接状态标签 |
| `yb_bg_status_waiting` | 等待状态标签 |
| `yb_bg_status_offline` | 离线状态标签 |
| `yb_bg_status_warning` | 温和提醒标签 |
| `yb_bg_status_danger` | 危险状态标签 |
| `yb_bg_chat_self` | 自己消息气泡 |
| `yb_bg_chat_peer` | 对方消息气泡 |
| `yb_bg_video_container` | 视频区域外层卡片背景，不替代真实 ImageView |
| `yb_bg_video_placeholder` | 视频等待、加载、错误占位背景 |

视频区域颜色建议：

| Token | HEX | 用途 | 禁止用途 |
| --- | --- | --- | --- |
| `yb_color_video_placeholder` | `#F1F2FA` | 视频等待、加载、错误占位背景 | 真实视频滤镜、遮罩 |

视频区域允许浅色占位背景；真实视频显示时不得叠加强紫色滤镜、渐变、透明遮罩或持续装饰动画。不得定义或建议新的播放器实现。

禁止意义不明的名字：`final_bg`、`new_bg`、`purple2`、`card_new`、`test_style`。

## 7. Style 命名建议

- `yb_style_Text_PageTitle`
- `yb_style_Text_SectionTitle`
- `yb_style_Text_Body`
- `yb_style_Text_Status`
- `yb_style_Button_Primary`
- `yb_style_Button_Secondary`
- `yb_style_Button_Danger`
- `yb_style_Card_Info`
- `yb_style_Card_Entry`
- `yb_style_Input_Outlined`

## 8. VectorDrawable 规范

不得新增第三方图标依赖。

正式功能图标要求：

- 24dp 基准；
- 统一视觉线宽；
- 统一圆角感；
- 支持 tint；
- 不使用 Emoji；
- 不使用表情包图片代替；
- 同类操作在患者端和监护人端使用同一图标语言。

建议建立的功能图标语义：

- `yb_ic_message`
- `yb_ic_location`
- `yb_ic_call`
- `yb_ic_video`
- `yb_ic_camera`
- `yb_ic_microphone`
- `yb_ic_settings`
- `yb_ic_back`
- `yb_ic_device`
- `yb_ic_sos`
- `yb_ic_home`
- `yb_ic_profile`
- `yb_ic_guardian`
- `yb_ic_ai`
- `yb_ic_visibility`
- `yb_ic_logout`

## 9. 视频流 Token 边界

Token 只能描述视频区域外层视觉，不得暗示新的播放实现。

允许定义：

- `yb_radius_video_container`
- `yb_size_video_min_height`
- `yb_color_video_placeholder`
- `yb_bg_video_container`
- `yb_bg_video_placeholder`

禁止定义或建议：

- WebView 播放器；
- 系统播放器；
- SurfaceView；
- TextureView；
- 自定义播放器；
- 替代 `iv_video` 或 `iv_video_stream` 的新控件。

视频真实显示仍由现有 ImageView + `MjpegStreamer` 链路承担。

## 10. 阶段 6 Token 实施边界

6.1 只允许建立设计 Token、通用 VectorDrawable 和基础视觉资源，不得提前重写具体页面。

允许修改文件：

- `app/src/main/res/values/colors.xml`
- `app/src/main/res/values/themes.xml`
- 必要时新增 `app/src/main/res/values/dimens.xml`
- 必要时新增 `app/src/main/res/values/styles.xml`
- 必要的通用 `app/src/main/res/drawable/yb_*`

禁止修改文件：

- Kotlin；
- 页面 XML；
- Gradle；
- Manifest；
- 网络、消息模型、后端、硬件；
- 业务文案；
- 截图和 build 产物。

### 默认冻结文件清单

- `GuardianActivity.kt`
- `VideoCallActivity.kt`
- `PatientActivity.kt`
- `MjpegStreamer.kt`
- `HardwareStreamManager.kt`
- `WebSocketManager.kt`
- `MessageModels.kt`
- `PreferenceManager.kt`
- `后端/main.py`
- `硬件/main_visual_service.py`
- `AndroidManifest.xml`

阶段 6.1 Token 实施不得修改上述任何文件。其他 UI 实施轮次也默认冻结上述文件，不得因添加 Token、样式、图标或容器而调整这些文件。如果发现视觉实施必须修改其中某个文件，必须停止当前任务并获得用户对具体文件的单独授权。

不得以“只改 tint”“只改 visibility”“只改绑定”为理由自行修改 Activity。视频相关控件的动态 visibility 和生命周期逻辑继续由现有 Kotlin 控制。该清单与 `UI_DESIGN_SPEC.md` 和 `UI_ACCEPTANCE_CHECKLIST.md` 具有相同约束等级。
