# SukiSU Ultra GKI 2.0 - OnePlus Ace (PGKM10)

为一加Ace (PGKM10, spacewar) 自动编译 SukiSU Ultra GKI 2.0 内核

## 📱 设备信息

- **设备名称**: OnePlus Ace (一加Ace)
- **设备代号**: spacewar / pickle
- **型号**: PGKM10
- **处理器**: MediaTek Dimensity 8100-MAX (MT6895)
- **内核版本**: 5.10.x
- **Android版本**: Android 13/14
- **架构**: GKI 2.0

## ✨ 功能特性

- 🔐 **SukiSU Ultra** - 基于KernelSU的高级Root解决方案
- 🧩 **KPM模块管理** - 内核模块动态加载
- 👻 **SUSFS完整支持** - 强大的文件系统隐藏能力
- ⚡ **GKI 2.0架构** - 更好的兼容性和可维护性
- 🛡️ **SELinux兼容** - 完整的SELinux策略支持

## 🚀 快速开始

### 使用GitHub Actions自动编译（推荐）

1. **Fork本仓库**
   ```
   点击页面右上角的 "Fork" 按钮
   ```

2. **启用GitHub Actions**
   - 进入你Fork的仓库
   - 点击 `Settings` → `Actions` → `General`
   - 允许 "All actions and reusable workflows"

3. **开始编译**
   - 点击 `Actions` 标签
   - 选择 "Build SukiSU Ultra GKI Kernel for OnePlus Ace"
   - 点击 `Run workflow`
   - 配置编译参数：
     - **Kernel version**: 5.10 (默认)
     - **Android version**: android13 (默认，适用于5.10内核)
     - **Enable KPM**: true ✅
     - **Enable SUSFS**: true ✅
     - **Custom name**: SukiSU-Ultra-OnePlus-Ace

4. **下载编译产物**
   - 编译完成后（约30-60分钟）
   - 在 `Actions` 页面点击对应的workflow运行
   - 在 `Artifacts` 部分下载ZIP包
   - 或在 `Releases` 页面获取发布版本

## 📲 刷入指南

### 前置条件
- ✅ 已解锁Bootloader
- ✅ 已安装自定义Recovery (TWRP/OrangeFox)
- ✅ 已备份原boot分区（重要！）

### Recovery刷入（推荐）

1. 下载编译好的 `SukiSU-Ultra-OnePlus-Ace-*.zip`
2. 将ZIP文件传输到手机内部存储
3. 重启到Recovery模式：
   ```bash
   adb reboot recovery
   ```
4. 在Recovery中选择 "Install" / "安装"
5. 选择下载的ZIP文件
6. 滑动确认刷入
7. 刷入完成后，清除Dalvik/ART缓存
8. 重启系统

### 安装SukiSU Manager

1. 从 [SukiSU Ultra Releases](https://github.com/SukiSU-Ultra/SukiSU-Ultra/releases) 下载最新的Manager APK
2. 安装APK到手机
3. 打开应用，授予必要权限
4. 验证Root状态和KernelSU版本

## 🔍 验证安装

```bash
# 检查内核版本
adb shell uname -a
# 输出应包含: SukiSU-Ultra-OnePlus-Ace

# 检查KernelSU状态
adb shell su -v
# 输出: KernelSU版本号

# 检查SUSFS状态
adb shell "dmesg | grep -i susfs"
# 应显示SUSFS初始化日志
```

## 🛠️ 配置选项

内核已启用以下配置：

| 配置项 | 状态 | 说明 |
|--------|------|------|
| CONFIG_KSU | ✅ | KernelSU核心 |
| CONFIG_KPM | ✅ | 内核模块管理 |
| CONFIG_KSU_SUSFS | ✅ | SUSFS文件系统隐藏 |
| CONFIG_KSU_SUSFS_HAS_MAGIC_MOUNT | ✅ | Magic Mount支持 |
| CONFIG_KSU_SUSFS_SUS_PATH | ✅ | 路径隐藏 |
| CONFIG_KSU_SUSFS_SUS_MOUNT | ✅ | 挂载隐藏 |
| CONFIG_KSU_SUSFS_SUS_KSTAT | ✅ | Kstat欺骗 |
| CONFIG_KSU_SUSFS_SPOOF_UNAME | ✅ | Uname欺骗 |

## ❓ 常见问题

### Q: 为什么使用GKI 2.0而不是厂商内核？
A: GKI 2.0提供更好的兼容性、稳定性和可维护性。更容易获取安全更新，且支持更广泛的模块生态。

### Q: 支持OTA升级吗？
A: 不支持。系统OTA会覆盖内核分区，升级后需要重新刷入。建议在OTA前备份当前内核。

### Q: 对性能和续航有影响吗？
A: 影响极小。KernelSU设计为低开销运行，日常使用几乎感觉不到差异。

### Q: 如何卸载？
A: 刷回原厂boot.img即可完全卸载：
```bash
fastboot flash boot stock_boot.img
```

### Q: SafetyNet/Play Integrity检测？
A: 需要配合Shamiko、LSPosed等隐藏模块使用，并正确配置SUSFS规则。

## 🐛 故障排除

### 无法开机（Bootloop）
1. 重启到Recovery
2. 恢复之前备份的boot.img
3. 或从官方包提取boot.img刷入

### Root权限未生效
1. 确认内核版本是否正确
2. 重新安装SukiSU Manager
3. 检查SELinux状态：`adb shell getenforce`

### 模块无法加载
1. 确认KPM已启用
2. 检查模块是否兼容当前内核版本
3. 查看日志：`dmesg | grep -i kpm`

## 📚 相关资源

- 🌟 [SukiSU Ultra](https://github.com/SukiSU-Ultra/SukiSU-Ultra) - 官方仓库
- 🔧 [KernelSU](https://github.com/tiann/KernelSU) - KernelSU项目
- 👻 [SUSFS](https://gitlab.com/simonpunk/susfs4ksu) - SUSFS for KernelSU
- 📱 [Android GKI](https://source.android.com/docs/core/architecture/kernel/generic-kernel-image) - GKI官方文档
- 🛠️ [AnyKernel3](https://github.com/osm0sis/AnyKernel3) - 刷机包工具

## ⚠️ 免责声明

- ⚠️ 本内核为第三方内核，刷入有风险
- ⚠️ 可能导致设备无法启动、数据丢失、保修失效
- ⚠️ 刷入前请务必备份重要数据
- ⚠️ 使用本内核即表示您了解并接受所有风险
- ⚠️ 作者不对任何损失负责

## 📄 许可证

- Linux Kernel: GPL-2.0
- KernelSU: GPL-3.0
- SukiSU Ultra: GPL-3.0
- 本项目: GPL-3.0

## 💖 致谢

感谢以下项目和开发者：

- [ShirkNeko](https://github.com/ShirkNeko) - SukiSU Ultra
- [tiann](https://github.com/tiann) - KernelSU
- [simonpunk](https://gitlab.com/simonpunk) - SUSFS
- [osm0sis](https://github.com/osm0sis) - AnyKernel3
- Google - Android GKI
- 所有贡献者和测试者

---

如果这个项目对您有帮助，请给个⭐Star支持一下！
