# Location Integrity

虚拟定位检测工具

[下载 APK](https://github.com/Lecheeel/LocationIntegrity/releases/latest)

## 能力

- GPS、Network、Passive、系统 Fused 定位观测。
- GNSS 卫星、NMEA、原始测量与传感器数据查看。
- 系统 Mock 标记与定位异常分析。
- 实验记录、时间线标记、两次实验对比与 JSON 导出。
- 回调间隔、内存与 CPU 使用情况观测。

## 构建

JDK 25、Gradle 9.7.0、Android SDK 37、Build-Tools 37.0.0。通过 local.properties 配置本机 SDK 路径。

    ./gradlew :integrity-core:test
    python -m unittest discover -s scripts -p 'test_verify_integrity_apk.py'
    ./gradlew :integrity-app:lint --max-workers=1
    ./gradlew :integrity-app:assembleDebug :integrity-app:assembleRelease :integrity-app:assembleDebugAndroidTest
