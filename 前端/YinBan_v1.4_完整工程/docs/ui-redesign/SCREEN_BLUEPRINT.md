# YinBan Screen Blueprint

本文件固化阶段 6 页面实施蓝图。唯一功能和逻辑基线为 v1.4、提交 `dc2ff0d`、当前工程实际 Kotlin/XML/ViewBinding、14 张真实运行截图。团队样图只决定视觉语言，不决定功能数量、控件数量或页面结构。

## 1. 页面文件总览

| 页面 | Kotlin 文件 | XML 文件 | 验收截图 |
| --- | --- | --- | --- |
| 登录角色选择 | `app/src/main/java/com/yinban/ai/ui/LoginActivity.kt` | `app/src/main/res/layout/activity_login.xml` | `01-login-role-default.png`、`02-login-role-patient.png`、`03-login-role-guardian.png` |
| 登录账号信息 | `LoginActivity.kt` | `activity_login.xml` | `04-login-account.png` |
| 登录设备配对 | `LoginActivity.kt` | `activity_login.xml` | `05-login-pair.png` |
| 患者首页 | `PatientActivity.kt`、`HomeFragment.kt` | `activity_patient.xml`、`fragment_home.xml` | `06-patient-home.png` |
| 小影火 AI | `PatientActivity.kt`、`ChatAiFragment.kt`、`ChatActivity.kt` | `activity_patient.xml`、`fragment_chatai.xml`、`activity_chat.xml` | `07-patient-ai.png` |
| 患者监护栏 | `PatientActivity.kt`、`GuardianFragment.kt` | `activity_patient.xml`、`fragment_guardian.xml` | `08-patient-guardian.png` |
| 患者“我的” | `PatientActivity.kt`、`MeFragment.kt` | `activity_patient.xml`、`fragment_me.xml` | `09-patient-me.png` |
| 离线聊天 | `ChatActivity.kt`、`ChatMessageAdapter.kt` | `activity_chat.xml`、`item_chat_message.xml` | `10-chat-offline.png` |
| SOS 确认弹窗 | `PatientActivity.kt`、`HomeFragment.kt` | `fragment_home.xml`；弹窗由 Kotlin 创建 | `11-sos-confirm.png` |
| 监护人首页 | `GuardianActivity.kt` | `activity_guardian.xml` | `12-guardian-home.png` |
| 监护人“我的” | `GuardianActivity.kt`、`MeFragment.kt` | `activity_guardian.xml`、`fragment_me.xml` | `13-guardian-me.png` |
| 音频通话 | `VideoCallActivity.kt` | `activity_video_call.xml` | `14-audio-call.png` |

## 2. 全局高风险控件核对

必须保留并在阶段 6 每轮核对：

- `bottom_nav`
- `fragment_container`
- `content_area`
- `guardian_main`
- `card_sos_alert`
- `iv_video`
- `tv_guardian_video_placeholder`
- `et_chat_input`
- `btn_send_message`
- `btn_voice_input`
- `switch_video`
- `switch_audio`
- `btn_sos`
- `btn_guardian_view_video`
- `btn_sos_view_video`
- `btn_guardian_audio_call`

以上 ID 可移动和重排，但不得删除、改名或断开绑定。

## 3. 登录角色选择

对应文件：`LoginActivity.kt`、`activity_login.xml`。

当前真实功能：

- 三步登录流程的第 1 步；
- 默认角色为 `patient`；
- 可选择患者端或监护人端；
- 确认身份进入第 2 步；
- 快速体验直接进入对应角色页面；
- 角色选择通过 `selectRole("patient")` / `selectRole("guardian")` 写入内部值。

最终页面区块顺序：

1. 品牌区：标题、说明、可使用 `开心.png`，但不改“AI 影伴系统”等现有文案。
2. 步骤条：`step_indicator`、`tv_step1_dot`、`tv_step2_dot`、`tv_step3_dot`。
3. 角色选择卡：`card_step1`。
4. 患者端卡：`card_role_patient`、`tv_check_patient`。
5. 监护人端卡：`card_role_guardian`、`tv_check_guardian`。
6. 主按钮：`btn_step1_confirm`。
7. 快速体验：`btn_skip_login`。

必须保留的控件 ID：

- `tv_login_title`
- `tv_login_subtitle`
- `step_indicator`
- `tv_step1_dot`
- `tv_step2_dot`
- `tv_step3_dot`
- `card_step1`
- `card_role_patient`
- `tv_check_patient`
- `card_role_guardian`
- `tv_check_guardian`
- `btn_step1_confirm`
- `btn_skip_login`

可移动但不可删除的控件：所有上述控件。

动态 visibility：`card_step1` 和 `btn_step1_confirm` 在第 1 步显示；第 2/3 步隐藏。`tv_check_patient` 与 `tv_check_guardian` 根据角色选择显示或隐藏。

状态：

- 正常：默认选中患者端。
- 连接/等待/离线/错误/空状态：不适用。

是否使用 `开心.png`：允许在品牌区使用，建议 64dp 至 96dp。

不允许加入的旧样图功能：事件记录、风险分析、支持者管理、通知铃铛。

不能修改的业务逻辑：`selectedRole`、快速体验、三步切换、角色值、跳转目标。

页面完成标准：功能入口、选中态、按钮、快速体验均保留；无 Emoji 功能图标；不出现“影行”；业务文案默认不改。

## 4. 登录账号信息

对应文件：`LoginActivity.kt`、`activity_login.xml`。

当前真实功能：

- 三步登录流程第 2 步；
- 输入账号、密码；
- Debug 构建可显示后端服务器 IP；
- 下一步校验后进入第 3 步；
- 返回重新选择角色。

最终页面区块顺序：

1. 品牌标题和步骤条。
2. 账号信息卡：`card_step2`。
3. 账号输入：`til_account`、`et_account`。
4. 密码输入：`til_password`、`et_password`。
5. 服务器 IP：`til_server_ip`、`et_server_ip`。
6. 下一步：`btn_step2_next`。
7. 返回：`btn_step2_back`。

必须保留的控件 ID：`card_step2`、`til_account`、`et_account`、`til_password`、`et_password`、`til_server_ip`、`et_server_ip`、`btn_step2_next`、`btn_step2_back`。

动态 visibility：`til_server_ip` 由 `BuildConfig.SHOW_SERVER_CONFIG` 控制；`card_step2`、`btn_step2_next`、`btn_step2_back` 只在第 2 步显示。

状态：

- 正常：账号、密码、IP 可输入。
- 错误：保持现有 TextInputLayout error 逻辑。
- 连接/等待/离线/空状态：不适用。

是否使用 `开心.png`：一般不使用；如品牌区全局保留，可小尺寸使用。

不允许加入的旧样图功能：事件筛选、风险标签、支持者联系人。

不能修改的业务逻辑：校验规则、Debug IP 显示条件、字段保存、下一步和返回行为。

页面完成标准：三个输入字段保持可用；错误提示逻辑不变；文案不润色、不替换。

## 5. 登录设备配对

对应文件：`LoginActivity.kt`、`activity_login.xml`。

当前真实功能：

- 三步登录流程第 3 步；
- 输入配对码；
- 配对码最长 6 位；
- 输入后保存账号、密码、房间号、角色、服务器 IP；
- 根据角色跳转患者端或监护人端；
- 返回修改信息。

最终页面区块顺序：

1. 标题和步骤条。
2. 配对卡：`card_step3`。
3. 配对说明：`tv_pairing_hint`。
4. 配对码输入：`til_room`、`et_room`。
5. 操作组：`group_step3_buttons`。
6. 进入：`btn_pair_enter`。
7. 返回：`btn_step3_back`。
8. 版本：`tv_version`。

必须保留的控件 ID：`card_step3`、`tv_pairing_hint`、`til_room`、`et_room`、`group_step3_buttons`、`btn_pair_enter`、`btn_step3_back`、`tv_version`。

动态 visibility：`card_step3` 和 `group_step3_buttons` 只在第 3 步显示。

状态：

- 正常：输入配对码。
- 错误：配对码为空或不足 3 位时显示原错误。
- 连接/等待/离线/空状态：不适用。

是否使用 `开心.png`：不建议作为配对功能图标。

不能修改的业务逻辑：`performLogin()`、`validateStep3()`、房间号保存、角色跳转。

页面完成标准：配对码输入、计数、进入、返回全部保留；功能图标使用 VectorDrawable。

## 6. 患者首页

对应文件：`PatientActivity.kt`、`HomeFragment.kt`、`activity_patient.xml`、`fragment_home.xml`。

当前真实功能：

- 顶部连接状态和房间号；
- 底部导航；
- 待命状态卡；
- 摄像头开关；
- 麦克风开关；
- 发送位置；
- 发送设备状态；
- SOS 紧急求助。

最终页面区块顺序：

1. 顶部连接状态：`banner_connection`、`dot_status`、`tv_connection_status`、`tv_room_number`。
2. Fragment 容器：`fragment_container`。
3. 主状态卡：`card_standby`、`tv_standby_title`、`tv_standby_subtitle`、`tv_daily_quote`。
4. 设备控制卡：`switch_video`、`switch_audio`。
5. 次级入口：`btn_send_location`、`btn_send_device_status`。
6. SOS：`btn_sos`。
7. 底部导航：`bottom_nav`。

必须保留的控件 ID：`banner_connection`、`dot_status`、`tv_connection_status`、`tv_room_number`、`fragment_container`、`bottom_nav`、`card_standby`、`tv_standby_title`、`tv_standby_subtitle`、`tv_daily_quote`、`switch_video`、`switch_audio`、`btn_send_location`、`btn_send_device_status`、`btn_sos`。

动态 visibility：连接状态由 `PatientActivity.updateConnectionBanner()` 更新；首页内容随底部导航替换 Fragment。

视频流保护：

| 控件 ID | 控件类型 | 正常 visibility | 动态 visibility | 不得改变的绑定 |
| --- | --- | --- | --- | --- |
| `switch_video` | 原开关控件类型 | 可见 | 随首页 Fragment 生命周期存在 | `HomeFragment.setupSwitch()` -> `HomeCallback.onVideoToggle()` -> `PatientActivity` 设备控制逻辑 |
| `switch_audio` | 原开关控件类型 | 可见 | 随首页 Fragment 生命周期存在 | `HomeFragment.setupSwitch()` -> `HomeCallback.onAudioToggle()` -> `PatientActivity` 设备控制逻辑 |

`switch_video` 和 `switch_audio` 是 `stream_start` / `stream_stop` 相关设备入口的前端触发控件，不得改 ID、控件类型、ViewBinding 对应关系、点击/切换绑定、enabled/disabled 状态处理或房间角色逻辑。

允许修改的外层样式：开关所在卡片的圆角、描边、内边距、背景、分割线和文字排版。不得为了美观将开关替换为静态按钮或图标。

真实视频验收步骤：

1. 改造前先用现有版本完成摄像头链路基线验收。
2. 患者端进入房间后切换 `switch_video`。
3. 确认后端收到原设备控制消息。
4. 确认设备服务可按原逻辑开启或停止摄像头。
5. 确认监护人请求画面后仍能收到 `stream_url` 并显示 MJPEG。

状态：

- 正常：展示待命、设备控制、位置、状态、SOS。
- 连接：使用 `status_connected`。
- 等待：使用 `status_waiting`。
- 离线：使用 `status_offline`。
- 错误：Snackbar 和连接错误保持原逻辑。
- 空状态：不适用，主状态卡仍存在。

是否使用 `开心.png`：允许在主状态卡小尺寸使用，建议 32dp 至 64dp。

不允许加入的旧样图功能：事件记录、风险分析、支持者管理。

不能修改的业务逻辑：开关回调、位置发送、设备状态发送、SOS 触发、底部导航。

页面完成标准：所有入口可见且可触发；SOS 醒目但不长期大面积高刺激；状态语义色正确。

## 7. 小影火 AI

对应文件：`PatientActivity.kt`、`ChatAiFragment.kt`、`ChatActivity.kt`、`fragment_chatai.xml`、`activity_chat.xml`。

当前真实功能：

- 患者端底部导航进入小影火页；
- `tv_ai_status` 展示 AI 状态；
- `btn_start_chat` 打开 `ChatActivity`，传入 `EXTRA_ROLE = patient`、`EXTRA_MODE = ai`；
- AI 聊天页在断网时仍可直连 DeepSeek HTTP。

最终页面区块顺序：

1. 顶部连接状态仍来自 `activity_patient.xml`。
2. AI 品牌主视觉，可使用 `开心.png`。
3. AI 状态：`tv_ai_status`。
4. 开始对话：`btn_start_chat`。
5. 聊天页顶部和输入区由 `activity_chat.xml` 承载。

必须保留的控件 ID：`tv_ai_status`、`btn_start_chat`、聊天页中的 `btn_chat_back`、`tv_chat_peer_name`、`rv_chat_messages`、`btn_voice_input`、`et_chat_input`、`btn_send_message`。

动态 visibility：AI 页本身无复杂 visibility；聊天页 `tv_offline_banner` 在手动聊天断开时显示，AI 模式断网仍可用。

状态：

- 正常：可开始对话。
- 连接：AI 聊天可显示在线。
- 等待：不适用。
- 离线：AI 模式直连仍可用，手动聊天离线禁用输入。
- 错误：AI 风险、连接错误、TTS 等逻辑保持。
- 空状态：聊天历史为空时显示欢迎语。

是否使用 `开心.png`：应使用，作为小影火 AI 页面主视觉，最多约 96dp。

不能修改的业务逻辑：`EXTRA_ROLE`、`EXTRA_MODE`、DeepSeek 兜底、AI 风险提示、消息发送和语音输入。

页面完成标准：AI 入口和聊天启动不变；功能图标无 Emoji；欢迎/风险/聊天文案默认不改。

## 8. 患者监护栏

对应文件：`PatientActivity.kt`、`GuardianFragment.kt`、`fragment_guardian.xml`。

当前真实功能：

- 消息入口；
- 位置入口；
- 通话入口；
- 画面入口；
- 最近消息；
- 位置状态。

最终页面区块顺序：

1. 2x2 功能入口区。
2. 消息：`card_shortcut_message`、`tv_unread_count`。
3. 位置：`card_shortcut_location`、`tv_location_status`。
4. 通话：`card_shortcut_call`。
5. 画面：`card_shortcut_video`。
6. 最近消息：`tv_recent_message`。

必须保留的控件 ID：`card_shortcut_message`、`tv_unread_count`、`card_shortcut_location`、`tv_location_status`、`card_shortcut_call`、`card_shortcut_video`、`tv_recent_message`。

动态 visibility：当前无主要 visibility；状态文本由 `refreshStatus()` 更新。

状态：

- 正常：四入口可点。
- 连接/等待/离线：由顶部连接状态和各入口说明表达。
- 空状态：最近消息显示现有“暂无消息”。
- 错误：走现有回调和 Snackbar。

是否使用 `开心.png`：一般不使用，最多可在空状态小尺寸使用；不得替代入口图标。

不能修改的业务逻辑：四个回调 `onOpenChat()`、`onOpenLocation()`、`onStartCall()`、`onViewStream()`。

页面完成标准：四入口不能合并、删除或弱化；不改为旧样图“支持者”结构。

## 9. 患者“我的”

对应文件：`PatientActivity.kt`、`MeFragment.kt`、`fragment_me.xml`。

当前真实功能：

- 头像和昵称；
- 账号；
- 角色标签；
- 振动提醒；
- 语音播报；
- DeepSeek API Key；
- 关于；
- 退出登录；
- 监护人角色下隐藏提示设置和 AI 设置。

最终页面区块顺序：

1. 账户卡：`avatar_container`、`iv_avatar_photo`、`tv_avatar`、`group_nickname`、`tv_profile_name`、`tv_profile_account`、`chip_role`。
2. 提示设置：`card_prompt_settings`、`switch_vibration`、`switch_voice`。
3. AI 设置：`card_ai_settings`、`group_api_key`、`tv_api_key_hint`。
4. 关于。
5. 退出：`btn_logout`。

必须保留的控件 ID：`avatar_container`、`iv_avatar_photo`、`tv_avatar`、`group_nickname`、`tv_profile_name`、`tv_profile_account`、`chip_role`、`card_prompt_settings`、`switch_vibration`、`switch_voice`、`card_ai_settings`、`group_api_key`、`tv_api_key_hint`、`btn_logout`。

动态 visibility：监护人角色下 `card_prompt_settings` 和 `card_ai_settings` 隐藏；头像照片和 Emoji 文本互斥显示。

状态：

- 正常：显示账号和角色。
- 空状态：昵称/API Key 未设置时保持现有文案。
- 错误：保存失败等逻辑不改。

是否使用 `开心.png`：不建议作为用户头像或功能图标。

不能修改的业务逻辑：角色判断、设置存储、API Key 设置、退出登录、头像逻辑。

页面完成标准：患者和监护人角色差异保留；设置项名称不改。

## 10. 离线聊天

对应文件：`ChatActivity.kt`、`ChatMessageAdapter.kt`、`activity_chat.xml`、`item_chat_message.xml`。

当前真实功能：

- 返回；
- 对方名称；
- 离线横幅；
- 聊天列表；
- 语音输入；
- 文本输入；
- 发送；
- 手动聊天离线时禁用输入和发送；
- AI 模式断网仍可直连使用。

最终页面区块顺序：

1. 顶部栏：`btn_chat_back`、`tv_chat_peer_name`。
2. 离线提示：`tv_offline_banner`。
3. 消息列表：`rv_chat_messages`、`tv_message_content`。
4. 输入栏：`btn_voice_input`、`et_chat_input`、`btn_send_message`。

必须保留的控件 ID：`btn_chat_back`、`tv_chat_peer_name`、`tv_offline_banner`、`rv_chat_messages`、`btn_voice_input`、`et_chat_input`、`btn_send_message`、`tv_message_content`。

动态 visibility：`tv_offline_banner` 连接时隐藏、断开时显示；输入控件在手动聊天离线时 disabled。

状态：

- 正常：输入可用。
- 连接：隐藏离线提示。
- 离线：显示离线提示，禁用输入和发送。
- 错误：连接错误 Toast/Snackbar 逻辑不改。
- 空状态：消息为空时保留空白聊天区或欢迎语。

是否使用 `开心.png`：可在空状态克制使用，不得替代语音或发送图标。

不能修改的业务逻辑：`EXTRA_ROLE`、`EXTRA_MODE`、消息发送、语音触摸、AI 兜底、离线禁用逻辑。

页面完成标准：离线状态清楚但不焦虑；禁用态明确；文案不改。

## 11. SOS 确认弹窗

对应文件：`PatientActivity.kt`、`HomeFragment.kt`、`fragment_home.xml`；弹窗由 Kotlin 创建。

当前真实功能：

- 点击 `btn_sos` 后出现确认弹窗；
- 弹窗说明将向监护人发送紧急求助并共享当前精确位置；
- 取消；
- 确定求助；
- 发送 SOS 后走原有 WebSocket/位置逻辑。

最终页面区块顺序：

1. 背景遮罩。
2. 弹窗卡片。
3. SOS 标题。
4. SOS 确认说明。
5. 取消。
6. 确定求助。

必须保留的控件 ID：入口 `btn_sos`。弹窗若在阶段 6 改为 XML 或自定义布局，必须不改变现有按钮语义和回调。

动态 visibility：弹窗按原逻辑显示/关闭。

状态：

- 正常：SOS 入口可点。
- 危险：使用 `status_danger`。
- 离线/错误：保持原有发送失败或提示逻辑。

是否使用 `开心.png`：不使用。

不能修改的业务逻辑：SOS 标题、确认说明、发送逻辑、位置共享逻辑、WebSocket 消息字段。

页面完成标准：二次确认仍存在；红色醒目但不压迫；文案完全保留。

## 12. 监护人首页

对应文件：`GuardianActivity.kt`、`activity_guardian.xml`。

当前真实功能：

- 顶部监护人状态和房间号；
- SOS 警报卡；
- 首页内容区；
- 实时数据；
- 患者消息；
- 视频画面；
- 查看画面；
- 消息；
- 语音；
- 底部导航；
- 我的页通过 `content_area` 替换。

最终页面区块顺序：

1. 顶部状态：`banner_status`、`dot_status`、`tv_guardian_connection`、`tv_guardian_room`。
2. SOS 卡：`card_sos_alert`、`tv_sos_message`、`tv_sos_location`、`btn_sos_view_video`、`btn_sos_dismiss`。
3. 内容区：`content_area`。
4. 首页主容器：`guardian_main`。
5. 数据卡：`card_dashboard`、`tv_location_lat`、`tv_location_lng`、`tv_location_accuracy`、`tv_camera_status`、`tv_headphone_status`、`tv_patient_message`。
6. 视频卡：`card_guardian_video`、`iv_video`、`tv_guardian_video_placeholder`。
7. 操作栏：`btn_guardian_view_video`、`btn_guardian_go_chat`、`btn_guardian_audio_call`。
8. 底部导航：`bottom_nav`。

必须保留的控件 ID：`banner_status`、`dot_status`、`tv_guardian_connection`、`tv_guardian_room`、`card_sos_alert`、`tv_sos_message`、`tv_sos_location`、`btn_sos_view_video`、`btn_sos_dismiss`、`content_area`、`guardian_main`、`card_dashboard`、`tv_location_lat`、`tv_location_lng`、`tv_location_accuracy`、`tv_camera_status`、`tv_headphone_status`、`tv_patient_message`、`card_guardian_video`、`iv_video`、`tv_guardian_video_placeholder`、`btn_guardian_view_video`、`btn_guardian_go_chat`、`btn_guardian_audio_call`、`bottom_nav`。

动态 visibility：

- `guardian_main` 在首页显示，在“我的”显示时隐藏。
- `card_sos_alert` 收到 SOS 或 AI 风险时显示，可 dismiss。
- `iv_video` 与 `tv_guardian_video_placeholder` 根据视频连接状态切换。

视频流保护：

当前真实链路为：

```text
硬件摄像头服务
-> 后端 WebSocket
-> device_control_request / stream_start / stream_stop
-> stream_url / stream_status
-> Android MjpegStreamer
-> ImageView 显示实时 MJPEG 画面
```

不得描述或改造为 WebView、系统播放器、SurfaceView、TextureView 或其他视频实现。

| 控件 ID | 控件类型 | 正常 visibility | 动态 visibility | 不得改变的绑定 |
| --- | --- | --- | --- | --- |
| `iv_video` | `ImageView` | 收到有效 MJPEG 帧后可见 | 等待/错误时隐藏，播放时显示 | `GuardianActivity.handleStreamUrl()` / `startMjpegStream()` / `setImageBitmap()` |
| `tv_guardian_video_placeholder` | `TextView` | 等待、请求、加载、错误时可见 | 收到 MJPEG 帧后隐藏 | `showVideoPlaceholder()` 与 MJPEG 回调 |
| `btn_guardian_view_video` | `MaterialButton` | 可见 | 按原 enabled 状态 | 点击发送 `device_control_request` |
| `btn_sos_view_video` | `MaterialButton` | SOS 卡显示时可见 | 随 `card_sos_alert` 显示/隐藏 | SOS 视频入口，沿用原视频请求逻辑 |

必须覆盖的状态：

- 占位状态：`tv_guardian_video_placeholder` 显示等待患者画面。
- 请求状态：点击 `btn_guardian_view_video` 后显示正在请求画面。
- 加载状态：收到 `stream_url` 后开始 MJPEG 连接。
- 显示状态：`tv_guardian_video_placeholder` 隐藏，`iv_video` 显示实时画面。
- 错误状态：视频流错误、断开或摄像头关闭时恢复 placeholder 文案。

允许修改的外层样式：`card_guardian_video` 的圆角、背景、描边和边距；视频区域合理高度；placeholder 字体、图标和排版；`btn_guardian_view_video` 和 `btn_sos_view_video` 的颜色、圆角、尺寸；视频容器与实时数据、操作按钮之间的间距。

不得修改 `iv_video`、`tv_guardian_video_placeholder`、`btn_guardian_view_video`、`btn_sos_view_video` 的 ID；不得改变 `iv_video` 的 ImageView 控件类型；不得把 ID 转移到外层卡片；不得新建同名控件替代原控件；不得删除后重新创建绑定关系；不得使用 WebView、SurfaceView、TextureView 或自定义播放器替换；不得为了美观将真实 ImageView 覆盖在装饰层下方。

真实视频验收步骤：

1. 启动后端。
2. 启动硬件 `main_visual_service.py`。
3. device 使用与患者、监护人相同房间号连接。
4. 患者端和监护人端进入同一房间。
5. 监护人点击请求画面。
6. 后端收到 `device_control_request`。
7. 设备开启摄像头。
8. 后端返回 `stream_url`。
9. `tv_guardian_video_placeholder` 隐藏。
10. `iv_video` 显示实时画面，宽高大于 0，未被遮挡。
11. 离开页面或停止请求后，视频流正确停止。

阶段 6.5 未连接真实设备服务时，只能完成视觉预验收，不能宣布最终通过。

状态：

- 正常：等待或连接患者。
- 连接：实时数据更新，视频可显示。
- 等待：等待患者连入。
- 离线：视频占位和状态说明。
- 错误：视频流错误、连接错误、设备状态错误保持现有逻辑。
- 空状态：患者消息为空显示原占位。

是否使用 `开心.png`：一般不使用，可在品牌角标极少量使用；不得替代功能图标。

不允许加入的旧样图功能：今日概览、新事件、高风险/待处理事件列表、事件详情、支持者管理。

不能修改的业务逻辑：WebSocket 监听、消息类型、视频流、SOS、通话、底部导航替换。

页面完成标准：监护人端所有入口保留；视频区域不再有强监控压迫感；状态语义色正确；真实设备服务下 `iv_video` 能显示动态 MJPEG，placeholder 和错误状态切换正确。

## 13. 监护人“我的”

对应文件：`GuardianActivity.kt`、`MeFragment.kt`、`activity_guardian.xml`、`fragment_me.xml`。

当前真实功能：

- 底部导航切到“我的”；
- `guardian_main` 隐藏；
- `content_area` 替换为 `MeFragment`；
- 监护人角色隐藏患者专属设置；
- 关于、退出登录保留；
- 监护人底部操作栏仍在 Activity 布局中。

最终页面区块顺序：

1. 监护人顶部状态。
2. `content_area` 中的账户卡。
3. 关于。
4. 退出登录。
5. 底部操作栏和底部导航。

必须保留的控件 ID：`content_area`、`guardian_main`、`bottom_nav`、`avatar_container`、`tv_profile_name`、`tv_profile_account`、`chip_role`、`btn_logout`。

动态 visibility：`guardian_main` 首页显示、我的隐藏；`card_prompt_settings` 和 `card_ai_settings` 在监护人角色下隐藏。

状态：

- 正常：显示监护人账号。
- 等待/离线：顶部状态仍可见。
- 空状态：账号为空保持原显示。

是否使用 `开心.png`：不建议。

不能修改的业务逻辑：底部导航、角色判断、退出登录。

页面完成标准：不得把“监护人端”改成“支持者端”；不得加入样图支持者管理。

## 14. 音频/视频通话

对应文件：`VideoCallActivity.kt`、`activity_video_call.xml`。

当前真实功能：

- 支持 `EXTRA_CALL_TYPE = audio` 或 `video`；
- 音频通话隐藏视频流和本地预览；
- 计时；
- 通话状态；
- 麦克风静音；
- 挂断；
- 切换摄像头；
- 视频模式可显示 MJPEG 流和错误占位。

最终页面区块顺序：

1. 远端视频/音频区域：`surface_remote`、`iv_video_stream`、`tv_call_placeholder`。
2. 本地预览：`surface_local`。
3. 计时：`tv_call_duration`.
4. 控制栏：`bar_call_controls`、`fab_mute`、`fab_hangup`、`fab_switch_camera`。
5. 状态：`tv_call_status`。

必须保留的控件 ID：`surface_remote`、`iv_video_stream`、`tv_call_placeholder`、`surface_local`、`tv_call_duration`、`bar_call_controls`、`fab_mute`、`fab_hangup`、`fab_switch_camera`、`tv_call_status`。

动态 visibility：音频模式隐藏 `iv_video_stream` 和 `surface_local`；视频模式显示视频流，占位随流状态切换。

视频流保护：

| 控件 ID | 控件类型 | 正常 visibility | 动态 visibility | 不得改变的绑定 |
| --- | --- | --- | --- | --- |
| `iv_video_stream` | `ImageView` | 视频模式播放时可见 | 音频模式隐藏；加载/错误时与 placeholder 配合 | `VideoCallActivity.startMjpegStream()` / `setImageBitmap()` |
| `tv_call_placeholder` | `TextView` | 音频模式、加载、错误时可见 | 视频流正常后可隐藏 | 通话模式和 MJPEG 回调 |
| `fab_mute` | `FloatingActionButton` | 可见 | 保持原 enabled 状态 | 静音按钮原点击逻辑 |
| `fab_hangup` | `FloatingActionButton` | 可见 | 保持原 enabled 状态 | 停止流并 finish 的原点击逻辑 |
| `fab_switch_camera` | `FloatingActionButton` | 可见 | 保持原 enabled 状态 | 切换摄像头原点击逻辑 |

允许修改的外层样式：通话背景、视频外层容器、控制栏间距、`tv_call_placeholder` 字体和排版、三个控制按钮颜色/大小/圆角/图标、视频区域合理高度和比例。

不得修改 `iv_video_stream` ID；不得改变 `iv_video_stream` 的 ImageView 控件类型；不得替换为 WebView、SurfaceView、TextureView 或自定义播放器；不得让音频模式下视频区域违反原隐藏逻辑；不得让返回或挂断后停止流逻辑失效；不得用纯色层、遮罩或文字覆盖真实画面。

真实视频验收步骤：

1. 音频通话模式下确认 `iv_video_stream` 和本地预览按原逻辑隐藏。
2. 视频模式下确认 `iv_video_stream` 显示真实 MJPEG。
3. 确认 `tv_call_duration` 正常计时。
4. 确认 `fab_mute`、`fab_hangup`、`fab_switch_camera` 正常。
5. 返回和挂断后视频正确停止。
6. 页面生命周期切换不崩溃。
7. 不出现有声音但画面被遮挡。
8. 不出现画面仍在后台持续拉流。

状态：

- 正常：音频通话中。
- 连接：视频流连接或音频进行。
- 等待：正在连接摄像头。
- 离线/错误：视频流连接失败或已断开。
- 空状态：音频模式中心说明。

是否使用 `开心.png`：不使用。

不能修改的业务逻辑：通话类型、计时、挂断、静音、摄像头切换、MJPEG 流。

页面完成标准：继承 YinBan 色彩和控件体系，不再是纯黑系统页；控制按钮逻辑不变；真实视频模式下 `iv_video_stream` 能显示动态 MJPEG，音频模式隐藏逻辑正常，退出后停止流。

## 15. 阶段 6 实施轮次

| 轮次 | 范围 | 允许修改文件 | 禁止修改文件 | 构建命令 | 截图清单 | 通过条件 | 回退边界 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 6.1 | 设计 Token 与基础资源 | values、通用 drawable、通用 VectorDrawable | Kotlin、页面 XML、Gradle、Manifest、业务文案 | `java -classpath .\gradle\wrapper\gradle-wrapper.jar org.gradle.wrapper.GradleWrapperMain assembleDebug` | 登录默认、患者首页、监护人首页 | 构建通过，未改页面结构 | 回退 values/drawable 新增改动 |
| 6.2 | 登录三步 | `activity_login.xml`、登录相关 drawable/vector | `LoginActivity.kt`、业务文案 | 同上 | 01-05 | 三步功能和文案不变 | 回退登录 XML/drawable |
| 6.3 | 患者首页 | `activity_patient.xml`、`fragment_home.xml`、相关视觉资源 | `PatientActivity.kt`、`HomeFragment.kt` 业务逻辑 | 同上 | 06、11 | 首页入口和 SOS 保留 | 回退患者首页 XML/资源 |
| 6.4 | 患者其他 Tab | `fragment_chatai.xml`、`fragment_guardian.xml`、`fragment_me.xml`、相关视觉资源 | Fragment Kotlin 逻辑 | 同上 | 07、08、09 | AI、监护栏、我的功能保留 | 回退对应 XML/资源 |
| 视频改造前基线门 | 位于 6.4 和 6.5 之间；不是 UI 实施轮次 | 不修改文件 | 不提交；不得修改 Kotlin、XML、视频链路或资源 | 不适用 | 监护人真实出画面截图 + 后端/硬件关键日志 | 通过后才允许修改监护人首页 | 无代码回退；失败则报告基线链路故障 |
| 6.5 | 监护人首页 | `activity_guardian.xml`、相关视觉资源 | `GuardianActivity.kt`、`MjpegStreamer.kt`、WebSocket、视频链路、SOS/通话逻辑 | 同上 | 12 + 真实视频截图/日志 | 数据、视频、消息、语音、SOS 保留；真实设备服务下视频通过 | 回退监护人首页 XML/资源 |
| 6.6 | 监护人“我的” | `fragment_me.xml` 的共享视觉修订、必要资源 | 角色判断、退出逻辑 | 同上 | 13 | 监护人角色差异保留 | 回退我的页 XML/资源 |
| 6.7 | 聊天、离线、SOS 与通话 | `activity_chat.xml`、`item_chat_message.xml`、`activity_video_call.xml`、弹窗视觉资源 | `ChatActivity.kt`、`VideoCallActivity.kt`、`MjpegStreamer.kt`、SOS 逻辑、视频链路、消息字段 | 同上 | 10、11、14 + 通话真实视频截图/日志 | 离线禁用、SOS 二次确认、通话控制保留；真实视频/音频模式通过 | 回退聊天/通话 XML/资源 |
| 6.8 | 最终统一与全量验收 | 仅视觉一致性修补 | 任何业务逻辑、功能结构 | 同上 | 01-14 全量 | 构建、截图、diff 全通过 | 回退本轮统一修补 |

### 视频改造前基线门

该门禁不是 UI 实施轮次，不修改任何文件，不产生代码提交。

目标：在监护人首页视频区域发生任何 UI 修改之前，验证当前基线版本的完整真实视频链路正常，并保存可供改造后比较的证据。

前置环境：

- 后端运行；
- `硬件/main_visual_service.py` 运行；
- device、patient、guardian 使用同一房间号；
- Android 患者端和监护人端能够正常连接；
- 使用当前未改造的视频界面。

必须验证的链路：

硬件摄像头服务
→ 后端 WebSocket
→ `device_control_request`
→ 设备开启摄像头
→ `stream_url` / `stream_status`
→ Android `MjpegStreamer`
→ `iv_video` 显示实时 MJPEG 画面。

必须完成的操作：

1. 启动后端。
2. 启动硬件视觉服务。
3. patient、guardian、device 进入同一房间。
4. 监护人点击 `btn_guardian_view_video`。
5. 确认后端收到 `device_control_request`。
6. 确认硬件服务开启画面。
7. 确认 Android 收到 `stream_url`。
8. 确认 `tv_guardian_video_placeholder` 隐藏。
9. 确认 `iv_video` 显示动态实时画面。
10. 离开页面或停止请求。
11. 确认视频流正确停止或释放。

必须保存的证据：

- 监护人页面真实出画面截图；
- 后端关键日志；
- 硬件服务关键日志；
- 使用的房间号、设备和运行环境；
- 当前 Git HEAD；
- 当前 `git status`。

不得把静态图片、占位图或黑屏截图视为成功。

通过条件：

- 请求画面按钮有效；
- 原控制消息发送成功；
- `stream_url` 正常到达；
- placeholder 正确隐藏；
- `iv_video` 显示真实动态画面；
- 页面退出后停止流正常；
- App 无崩溃；
- Git 工作区未产生非预期代码改动。

如果该门禁失败：

- 不得进入 6.5；
- 不得通过修改 UI 或 Kotlin 绕过；
- 必须先报告基线链路故障。

每轮 Git diff 检查必须确认：不包含 Gradle、Manifest、网络层、消息模型、后端、硬件、截图、build 产物和 `.idea` 污染。

视频相关 Git diff 门槛：每次改动监护人首页、患者摄像头入口或通话页后必须执行 `git diff --name-only` 和 `git diff`。如 diff 出现 `GuardianActivity.kt`、`VideoCallActivity.kt`、`PatientActivity.kt`、`MjpegStreamer.kt`、`HardwareStreamManager.kt`、`WebSocketManager.kt`、`MessageModels.kt`、`PreferenceManager.kt`、`后端/main.py`、`硬件/main_visual_service.py` 或 `AndroidManifest.xml`，默认判定越界并停止，除非用户已针对具体文件给予单独明确授权。
