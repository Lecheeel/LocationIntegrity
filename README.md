# Location Integrity

独立 Android 定位证据观测与实验对比工具。无需 Root、无需 Xposed，也无需成为模拟位置应用。

[下载 APK](https://github.com/Lecheeel/LocationIntegrity/releases/latest) · [使用、数据与能力边界](docs/location-integrity.md)

## 能力

- GPS / Network / Passive / 系统 Fused 定位观测，区分缓存与实时样本、订阅渠道与位置对象来源。
- GNSS 卫星、NMEA、原始测量与时钟快照，加速度计和陀螺仪最新向量。
- 系统 Mock 标记与可解释异常证据；缺失数据不等于模拟，未发现异常不证明定位真实。
- 普通定位权限即可使用；近似权限自动降级，不申请后台位置、网络、模拟位置或全应用查询权限。
- 本地实验保存、手动时间线、两次实验对比与 JSON 导出。默认仅本机存储，不联网上传。
- 有界内存保留、实际回调间隔统计、进程 PSS / CPU 观测；不是无限原始数据录制器。

## 工程

- integrity-app：独立安装的 Android 应用，包名 io.github.lecheeel.locationintegrity，Android 8 / API 26 起。
- integrity-core：纯 Kotlin 数据模型、分析规则与 JVM 测试。
- scripts：APK 验证、签名管理与可丢弃模拟器上的设备测试。

JDK 25、Gradle 9.7.0、Android SDK 37 与 Build-Tools 37.0.0。local.properties 配置本机 SDK 路径。

    ./gradlew :integrity-core:test
    python -m unittest discover -s scripts -p 'test_verify_integrity_apk.py'
    ./gradlew :integrity-app:lint --max-workers=1
    ./gradlew :integrity-app:assembleDebug :integrity-app:assembleRelease :integrity-app:assembleDebugAndroidTest

Windows 使用 gradlew.bat。默认本地 Release 未签名，Debug 带 .debug 包名。

## 签名与发布

GitHub Actions 对核心规则、APK 内容/权限、lint 和 API 35 设备测试设门禁，通过后由版本标签签名发布。
仓库使用四个 INTEGRITY_KEY* Secrets，不提交私钥。公开证书 SHA-256 固定在 integrity-app/release-certificate.sha256。
本机签名恢复材料保存在仓库外，并由 Windows DPAPI 保护；本机签名构建与密钥管理详见使用文档。

## 边界

本工具展示自身收到的数据；系统或进程 Hook 可能同时改变这些数据，其他应用的定向伪造也可能不可见。
尚未建立实机误报/漏报率与厂商兼容率基准。导出的报告包含坐标与设备信息，请按需分享。
