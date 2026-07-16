# YinBan UI Acceptance Checklist

本清单用于阶段 6 每轮实施和阶段 6.8 全量验收。验收基线为 v1.4、提交 `dc2ff0d`、当前工程实际 Kotlin/XML/ViewBinding、14 张真实运行截图。

## P0. 视频流验收门

视频流是最高优先级验收门。只要视频验收失败，对应阶段立即判定为不通过，即使构建成功、截图好看也不能通过。

当前真实链路必须保持：

```text
硬件摄像头服务
-> 后端 WebSocket
-> device_control_request / stream_start / stream_stop
-> stream_url / stream_status
-> Android MjpegStreamer
-> ImageView 显示实时 MJPEG 画面
```

不得改造成 WebView、系统播放器、SurfaceView、TextureView 或其他视频实现。

默认冻结文件检查：

- [ ] `app/src/main/java/com/yinban/ai/ui/GuardianActivity.kt` 未修改。
- [ ] `app/src/main/java/com/yinban/ai/ui/VideoCallActivity.kt` 未修改。
- [ ] `app/src/main/java/com/yinban/ai/ui/PatientActivity.kt` 未修改。
- [ ] `app/src/main/java/com/yinban/ai/hardware/MjpegStreamer.kt` 未修改。
- [ ] `app/src/main/java/com/yinban/ai/hardware/HardwareStreamManager.kt` 未修改。
- [ ] `app/src/main/java/com/yinban/ai/network/WebSocketManager.kt` 未修改。
- [ ] `app/src/main/java/com/yinban/ai/network/MessageModels.kt` 未修改。
- [ ] `app/src/main/java/com/yinban/ai/storage/PreferenceManager.kt` 未修改。
- [ ] `后端/main.py` 未修改。
- [ ] `硬件/main_visual_service.py` 未修改。
- [ ] `app/src/main/AndroidManifest.xml` 未修改。

控件 ID 和控件类型检查：

- [ ] `iv_video` ID 未改，控件类型仍为 ImageView。
- [ ] `iv_video_stream` ID 未改，控件类型仍为 ImageView。
- [ ] `tv_guardian_video_placeholder` ID 未改，控件类型仍为 TextView。
- [ ] `btn_guardian_view_video` ID 未改。
- [ ] `btn_sos_view_video` ID 未改。
- [ ] `switch_video` ID 未改，控件类型仍为原开关体系。
- [ ] `switch_audio` ID 未改，控件类型仍为原开关体系。
- [ ] 原 ViewBinding 对应关系未改变。
- [ ] 原点击事件绑定未改变。
- [ ] 原 visibility 动态切换未改变。
- [ ] 原 enabled / disabled 状态未改变。
- [ ] 占位文字和真实画面的切换关系未改变。
- [ ] 音频模式下视频区域的隐藏逻辑未改变。
- [ ] 离开页面后的停止流逻辑未改变。

改造前视频基线验收：

- [ ] 启动后端。
- [ ] 启动硬件 `main_visual_service.py`。
- [ ] device 使用与患者、监护人相同房间号连接。
- [ ] 患者端和监护人端进入同一房间。
- [ ] 监护人点击请求画面。
- [ ] 后端收到 `device_control_request`。
- [ ] 设备开启摄像头。
- [ ] 后端返回 `stream_url`。
- [ ] `tv_guardian_video_placeholder` 隐藏。
- [ ] `iv_video` 显示实时画面。
- [ ] 离开页面或停止请求后，视频流正确停止。
- [ ] 已保留改造前截图和关键日志。

阶段 6.5 监护人首页改造后强制验收：

- [ ] 请求画面按钮仍可点击。
- [ ] 点击事件仍发送原消息。
- [ ] 等待时 placeholder 正常显示。
- [ ] `stream_url` 到达后 placeholder 隐藏。
- [ ] `iv_video` 正常显示动态画面。
- [ ] 画面尺寸非 0。
- [ ] 画面没有被卡片、遮罩或文字覆盖。
- [ ] 流失败时仍显示原错误状态。
- [ ] SOS 视频入口仍可用。
- [ ] 切换到底部“我的”再返回后页面状态合理。
- [ ] 退出页面后没有持续异常占用视频流。
- [ ] 未连接真实设备服务时，仅标记视觉预验收，不宣布阶段 6.5 最终通过。

阶段 6.7 通话页改造后强制验收：

- [ ] 音频通话模式下视频区域按原逻辑隐藏。
- [ ] 视频模式下 `iv_video_stream` 显示真实 MJPEG。
- [ ] 通话计时正常。
- [ ] 麦克风按钮正常。
- [ ] 挂断按钮正常。
- [ ] 摄像头按钮正常。
- [ ] 返回和挂断后视频正确停止。
- [ ] 页面生命周期切换不导致崩溃。
- [ ] 不出现有声音但画面被遮挡。
- [ ] 不出现画面仍在后台持续拉流。

视频功能阶段通过标准：

- [ ] `assembleDebug` 构建成功。
- [ ] App 无崩溃。
- [ ] 控件 ID 和类型未改变。
- [ ] ViewBinding 未改变。
- [ ] 请求画面消息仍发送。
- [ ] `stream_url` 仍能接收。
- [ ] placeholder 能正确切换。
- [ ] `iv_video` 能显示真实画面。
- [ ] `iv_video_stream` 能显示真实画面。
- [ ] 音频模式隐藏逻辑正常。
- [ ] 停止和退出后视频流正确结束。
- [ ] Git diff 未越界。
- [ ] 对应真实运行截图和必要日志已经保存。

## A. 功能不变

每轮必须检查：

- [ ] 所有原功能入口仍存在。
- [ ] 所有点击事件仍触发原逻辑。
- [ ] `patient` / `guardian` 值不变。
- [ ] 页面跳转不变。
- [ ] WebSocket 不变。
- [ ] 消息类型和字段不变。
- [ ] SOS 逻辑和文案不变。
- [ ] AI 逻辑不变。
- [ ] 摄像头逻辑不变。
- [ ] 麦克风逻辑不变。
- [ ] 位置逻辑不变。
- [ ] 设备状态逻辑不变。
- [ ] 设置存储不变。
- [ ] 快速体验仍可进入对应角色。
- [ ] 登录三步仍按原顺序切换。
- [ ] 监护人首页和“我的”切换仍通过原导航逻辑完成。

关键 ID 保留检查：

- [ ] `bottom_nav`
- [ ] `fragment_container`
- [ ] `content_area`
- [ ] `guardian_main`
- [ ] `card_sos_alert`
- [ ] `iv_video`
- [ ] `tv_guardian_video_placeholder`
- [ ] `et_chat_input`
- [ ] `btn_send_message`
- [ ] `btn_voice_input`
- [ ] `switch_video`
- [ ] `switch_audio`
- [ ] `btn_sos`
- [ ] `btn_guardian_view_video`
- [ ] `btn_sos_view_video`
- [ ] `btn_guardian_audio_call`

## B. 视觉一致

- [ ] 使用正式色彩 Token。
- [ ] `#5B5CEB` 是唯一主色。
- [ ] 没有新增其他品牌紫色。
- [ ] 没有自行调整已确认 HEX。
- [ ] 页面背景主要使用 `#F7F7FC` 和 `#FFFFFF`。
- [ ] 紫色只用于主按钮、选中态、底部导航选中项、少量品牌区域和重点交互。
- [ ] 红色只用于 SOS、危险确认和真正高风险状态。
- [ ] 在线、等待、离线分别使用对应语义色。
- [ ] 状态栏不再长期使用整块高饱和紫色背景。
- [ ] 卡片圆角统一。
- [ ] 描边和阴影统一。
- [ ] 字体层级统一。
- [ ] 功能图标无 Emoji。
- [ ] 功能图标使用统一 VectorDrawable。
- [ ] `开心.png` 使用符合规范。
- [ ] `开心.png` 没有被用作功能图标。
- [ ] 其他表情包图片没有被 Codex 自行加入页面。
- [ ] 不儿童化。
- [ ] 不医疗化。
- [ ] 不产生监控后台感。
- [ ] 不出现大面积高刺激紫色或红色。
- [ ] 不出现大面积高饱和渐变。
- [ ] 不出现强发光、装饰球、星光或无意义玻璃拟态。
- [ ] 不出现样图中的不存在功能。
- [ ] 不出现“影行”。

## C. 业务文案不变

默认禁止修改业务文案。每轮检查：

- [ ] “AI 影伴系统”等现有展示文案未被自行缩写为“影伴”。
- [ ] “患者端”未被改成“用户端”。
- [ ] “监护人端”未被改成“支持者端”。
- [ ] 服务器 IP 文案不变。
- [ ] 配对码文案不变。
- [ ] 房间号文案不变。
- [ ] 连接状态文案不变。
- [ ] 等待状态文案不变。
- [ ] 离线状态文案不变。
- [ ] SOS 标题和确认说明不变。
- [ ] AI 风险提示不变。
- [ ] 跨端消息不变。
- [ ] 设置项名称不变。
- [ ] 通话状态不变。
- [ ] 设备控制提示不变。
- [ ] 视频流错误提示不变。
- [ ] 没有根据样图添加事件记录、风险分析、支持者管理等不存在文案。

允许检查项：

- [ ] 仅调整字号、行高、换行、控件宽度、间距或文字位置。

## D. 设备与状态适配

至少检查：

- [ ] 1080x2400 视口。
- [ ] 状态栏。
- [ ] 系统导航栏。
- [ ] 键盘弹出。
- [ ] 输入框聚焦。
- [ ] 长文案。
- [ ] 在线状态。
- [ ] 等待状态。
- [ ] 离线状态。
- [ ] 错误状态。
- [ ] 空状态。
- [ ] SOS 弹窗。
- [ ] 监护人视频占位区。
- [ ] 音频通话页。
- [ ] 患者底部导航。
- [ ] 监护人底部导航。

## E. 截图验收清单

阶段 6.1：

- [ ] `01-login-role-default.png` 对应页面不破坏。
- [ ] `06-patient-home.png` 对应页面不破坏。
- [ ] `12-guardian-home.png` 对应页面不破坏。

阶段 6.2：

- [ ] `01-login-role-default.png`
- [ ] `02-login-role-patient.png`
- [ ] `03-login-role-guardian.png`
- [ ] `04-login-account.png`
- [ ] `05-login-pair.png`

阶段 6.3：

- [ ] `06-patient-home.png`
- [ ] `11-sos-confirm.png`

阶段 6.4：

- [ ] `07-patient-ai.png`
- [ ] `08-patient-guardian.png`
- [ ] `09-patient-me.png`

阶段 6.5：

- [ ] `12-guardian-home.png`

阶段 6.6：

- [ ] `13-guardian-me.png`

阶段 6.7：

- [ ] `10-chat-offline.png`
- [ ] `11-sos-confirm.png`
- [ ] `14-audio-call.png`

阶段 6.8：

- [ ] 01-14 全量截图全部重新验收。

## F. Git 与修改范围

每轮必须检查：

- [ ] 构建成功。
- [ ] `git diff` 只包含本轮允许范围。
- [ ] 不包含 Gradle。
- [ ] 不包含 Manifest。
- [ ] 不包含网络层。
- [ ] 不包含消息模型。
- [ ] 不包含后端。
- [ ] 不包含硬件。
- [ ] 不包含 `.idea` 污染。
- [ ] 不包含截图。
- [ ] 不包含 build 产物。
- [ ] 每轮可独立回退。

视频相关 diff 门槛：

- [ ] 已执行 `git diff --name-only`。
- [ ] 已执行 `git diff`。
- [ ] diff 未出现 `GuardianActivity.kt`。
- [ ] diff 未出现 `VideoCallActivity.kt`。
- [ ] diff 未出现 `PatientActivity.kt`。
- [ ] diff 未出现 `MjpegStreamer.kt`。
- [ ] diff 未出现 `HardwareStreamManager.kt`。
- [ ] diff 未出现 `WebSocketManager.kt`。
- [ ] diff 未出现 `MessageModels.kt`。
- [ ] diff 未出现 `PreferenceManager.kt`。
- [ ] diff 未出现 `后端/main.py`。
- [ ] diff 未出现 `硬件/main_visual_service.py`。
- [ ] diff 未出现 `AndroidManifest.xml`。
- [ ] 如出现上述文件，已有用户针对该具体文件的单独明确授权；否则立即停止。

推荐构建命令：

```powershell
java -classpath .\gradle\wrapper\gradle-wrapper.jar org.gradle.wrapper.GradleWrapperMain assembleDebug
```

## G. 阶段 6 八轮通过条件

### 6.1 设计 Token 与基础资源

- 允许修改：values、通用 drawable、通用 VectorDrawable。
- 禁止修改：Kotlin、页面 XML、Gradle、Manifest、业务文案。
- 截图：登录默认、患者首页、监护人首页。
- 通过条件：构建成功，页面未因资源替换崩溃。
- 回退边界：回退本轮 values/drawable 新增或修改。

### 6.2 登录三步

- 允许修改：`activity_login.xml`、登录相关 drawable/vector。
- 禁止修改：`LoginActivity.kt`、登录逻辑、业务文案。
- 截图：01-05。
- 通过条件：三步流程、角色选择、快速体验、IP、配对码全部不变。
- 回退边界：回退登录 XML 和登录视觉资源。

### 6.3 患者首页

- 允许修改：`activity_patient.xml`、`fragment_home.xml`、相关视觉资源。
- 禁止修改：`PatientActivity.kt`、`HomeFragment.kt` 业务逻辑。
- 截图：06、11。
- 通过条件：摄像头、麦克风、位置、状态、SOS 全部保留。
- 回退边界：回退患者首页 XML 和资源。

### 6.4 患者其他 Tab

- 允许修改：`fragment_chatai.xml`、`fragment_guardian.xml`、`fragment_me.xml`、相关视觉资源。
- 禁止修改：Fragment Kotlin 逻辑、AI Key 保存、聊天跳转。
- 截图：07、08、09。
- 通过条件：AI、四个监护栏入口、我的设置全部保留。
- 回退边界：回退对应 XML 和资源。

### 6.5 监护人首页

- 允许修改：`activity_guardian.xml`、相关视觉资源。
- 禁止修改：`GuardianActivity.kt`、`MjpegStreamer.kt`、WebSocket、视频链路、SOS、通话逻辑。
- 截图：12，以及真实视频运行截图和必要日志。
- 通过条件：实时数据、患者消息、视频画面、请求画面、消息、语音、SOS 全部保留；真实设备服务下视频流验收门通过。
- 回退边界：回退监护人首页 XML 和资源。

### 6.6 监护人“我的”

- 允许修改：`fragment_me.xml` 的共享视觉修订和必要资源。
- 禁止修改：角色判断、退出逻辑、监护人底部导航。
- 截图：13。
- 通过条件：监护人角色差异和退出登录保留。
- 回退边界：回退我的页 XML 和资源。

### 6.7 聊天、离线、SOS 与通话

- 允许修改：`activity_chat.xml`、`item_chat_message.xml`、`activity_video_call.xml`、弹窗视觉资源。
- 禁止修改：`ChatActivity.kt`、`VideoCallActivity.kt`、`MjpegStreamer.kt`、SOS 逻辑、视频链路、消息字段。
- 截图：10、11、14，以及通话真实视频运行截图和必要日志。
- 通过条件：离线禁用、SOS 二次确认、通话控制和计时保留；音频模式和视频模式的视频流验收门通过。
- 回退边界：回退聊天、弹窗、通话 XML 和资源。

### 6.8 最终统一与全量验收

- 允许修改：仅视觉一致性修补。
- 禁止修改：任何业务逻辑、功能结构、业务文案。
- 截图：01-14 全量。
- 通过条件：构建通过、全量截图通过、diff 范围通过。
- 回退边界：回退本轮统一修补。

## H. 阶段 5 文档验收

- [ ] 只创建或更新四份 Markdown 文档。
- [ ] 未修改 Kotlin。
- [ ] 未修改 XML。
- [ ] 未修改 drawable。
- [ ] 未修改 values。
- [ ] 未修改 menu。
- [ ] 未修改 mipmap。
- [ ] 未修改 Gradle。
- [ ] 未修改 Manifest。
- [ ] 未修改后端。
- [ ] 未修改硬件。
- [ ] 未修改业务文案。
- [ ] 未运行 Git 提交。
- [ ] 未推送 GitHub。
