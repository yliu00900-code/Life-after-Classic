# LifeAfter Classic

一个以2018年《明日之后》第一季为灵感目标的原创3D生存游戏复刻项目。目标是还原经典第三人称手游的氛围与玩法循环，并最终提供可离线运行的安卓版本。

> 独立爱好者项目，不隶属于网易；不包含官方客户端、官方源代码或未经授权的游戏素材。地图、角色、剧情、美术与音频需使用原创或合法授权内容。

## 当前开发目标：V0.9 Android 工程化

现有原型包含：
- Three.js 第三人称3D森林场景、手机虚拟摇杆与触屏视角
- 树木/石块采集、背包、制作、营地建造
- 感染者巡逻、追击与近战战斗
- 饥饿、口渴、体温、昼夜与天气
- 幸存者NPC、无线电线索和主线任务

本次工程化更新：
- 使用 Vite + npm 管理项目依赖，Three.js 改为本地 npm 依赖，不再从运行时 CDN 加载
- 将原有游戏模块拆分为 `src/main.js`
- 增加 Capacitor Android 容器配置
- 增加 GitHub Actions 工作流，自动构建 Android debug APK
- 增加 PWA manifest 与基础 Service Worker 缓存（网页托管时使用）

## 本地开发

需要 Node.js 20 和 npm：

```bash
npm install
npm run dev
npm run build
```

## Android APK 构建

需要 Android SDK、JDK 17 和 Node.js 20：

```bash
npm install
npm run build
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug
```

也可以在 GitHub 仓库的 Actions 页面手动运行 **Android debug APK** 工作流。成功后，从该次工作流的 Artifacts 下载 `LifeAfter-Classic-debug-apk`。Debug APK 仅用于测试，不是签名发布版。

## 离线说明

Android APK 会把构建后的网页代码与 Three.js 依赖打包进应用，不需要游戏运行时访问 CDN。现阶段游戏资源主要由代码生成，后续新增模型、贴图、音频也必须随应用本地打包。存档目前使用浏览器/应用 WebView 的 localStorage；卸载应用或清除应用数据可能删除存档。

## 开发路线

- [x] 原型：3D森林、移动、采集、生存、感染者、制作、建造、NPC和任务
- [x] 工程化：Vite、本地 Three.js 依赖、Capacitor 配置、APK CI 工作流
- [ ] V0.9：首次 CI 构建验证、安卓真机触控/性能测试、存档迁移与备份
- [ ] V1.0：离线 APK 测试版、资源管理和稳定性优化
- [ ] 后续：扩展原创的秋日森林、远星城风格区域、沙石堡风格区域及更多装备/庄园内容

## 开源许可

原创代码采用 MIT License（见 `LICENSE`）。第三方依赖与素材遵循各自许可证。未经授权不得分发官方客户端、反编译得到的专有代码或官方美术/音频资源。
