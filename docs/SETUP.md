# Before you start

[← Home](../README.md) · [FAQ](FAQ.md)

**On Android 11, skip this page.** On Android 12 and later, complete these settings to reduce interruptions while Linux is running.

## Set up your phone

1. Open **LinDesk → Settings → Before you start** and follow the guide to enable your phone's **Developer options**.
2. Find **Disable child process restrictions** and turn it **ON**. Turning it on removes the restriction. It is a different setting from **Background process limit**.
3. Keep the main **Developer options switch ON**, return to LinDesk Home and start the desktop or terminal.

If LinDesk still says “not confirmed,” check that you have completed the settings, then confirm them manually as prompted.

<a id="computer-method"></a>
<details>
<summary>Can't find the switch? Set it up with a computer</summary>

Install [Android Platform-Tools](https://developer.android.com/tools/releases/platform-tools) on your computer. Enable **USB debugging** on the phone, connect it by USB and accept the debugging prompt. Run all commands below in a terminal **on your computer**.

Connect only the phone you want to set up, then check that its status is `device`:

```bash
adb devices
```

Check its Android version:

```bash
adb shell getprop ro.build.version.sdk
```

Run **only the commands that match the result**:

**32 or higher — Android 12L and later**

```bash
adb shell settings put global settings_enable_monitor_phantom_procs false
adb shell settings get global settings_enable_monitor_phantom_procs
```

The final result should be `false`.

**31 — Android 12.0**

```bash
adb shell device_config put activity_manager max_phantom_processes 2147483647
adb shell device_config get activity_manager max_phantom_processes
```

The final result should be `2147483647`. This only reduces some interruptions on Android 12.0, and the system may restore the value. Recheck it if unexpected shutdowns return.

Return to LinDesk, check **Before you start**, then start the desktop or terminal. If a command fails, keep the error message for troubleshooting.

</details>

[Still having trouble? See the FAQ](FAQ.md#troubleshooting)
