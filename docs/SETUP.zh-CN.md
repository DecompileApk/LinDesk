# 首次运行前设置

[← 返回首页](../README.zh-CN.md) · [常见问题](FAQ.zh-CN.md)

**Android 11 可跳过本页。** Android 12 及以上请完成以下设置，减少 Linux 运行时被系统中断的情况。

## 在手机上设置

1. 打开 **LinDesk → 设置 → 运行前设置**，按引导开启手机的**开发者选项**。
2. 在开发者选项中找到**停止限制子进程**（**Disable child process restrictions**），将它设为**开启**。这里开启代表解除限制，注意与“后台进程限制”区分。
3. 保持**开发者选项总开关开启**，返回 LinDesk 首页，启动桌面或终端。

如果仍显示“尚未确认”，请先核实设置已完成，再按页面提示手动确认。

<a id="computer-method"></a>
<details>
<summary>找不到“停止限制子进程”？展开电脑设置方法</summary>

在电脑安装 [Android Platform-Tools](https://developer.android.com/tools/releases/platform-tools)。手机开启 **USB 调试**，用数据线连接电脑，并同意调试授权。以下命令都在**电脑终端**执行。

只连接需要设置的这一台手机，确认状态为 `device`：

```bash
adb devices
```

查询系统版本：

```bash
adb shell getprop ro.build.version.sdk
```

根据结果，**只执行对应的一组命令**：

**结果为 32 或更大（Android 12L 及以上）**

```bash
adb shell settings put global settings_enable_monitor_phantom_procs false
adb shell settings get global settings_enable_monitor_phantom_procs
```

最后显示 `false`，表示设置成功。

**结果为 31（Android 12.0）**

```bash
adb shell device_config put activity_manager max_phantom_processes 2147483647
adb shell device_config get activity_manager max_phantom_processes
```

最后应显示 `2147483647`。Android 12.0 的方法只能缓解部分中断，系统也可能恢复原值；如果再次意外退出，请重新检查。

完成后返回 LinDesk，查看运行前设置，再启动桌面或终端。命令报错时请保留错误提示，方便排查。

</details>

[设置后仍有问题？查看常见问题](FAQ.zh-CN.md#troubleshooting)
