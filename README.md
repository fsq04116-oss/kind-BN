# kind BN

**kind BN** is an Android Root Shell utility designed for advanced Android users, module developers, and power users who need a clean, professional interface for running shell scripts, managing root-related modules, and testing APK signing workflows.

> Package name: `bn.bnstr.kind`

## Overview

kind BN provides a lightweight, Termux-style shell execution experience inside an Android application.  
It focuses on script execution, root environment compatibility, module inspection, terminal interaction, and basic script protection.

The project is built with:

- Kotlin
- Jetpack Compose
- Material 3
- Android Gradle Plugin
- Root / `su` command integration

## Key Features

### MT-style Shell / Binary Runner

kind BN includes an enhanced shell runner designed to execute different types of files commonly used in Android root environments.

Supported execution targets include:

- Standard `.sh` scripts
- Bash scripts
- Shebang-based scripts
- ELF binaries
- Packed shell/C binary tools
- Scripts located under `/data/adb`
- Custom working directories

The runner supports multiple execution modes:

- `AUTO`
- `SH`
- `BASH`
- `DIRECT`

In `AUTO` mode, the app tries to detect the best execution method based on the file type, extension, shebang header, or binary signature.

### Environment Injection

The execution layer injects a root-friendly shell environment, including:

```sh
PATH=/system/bin:/system/xbin:/vendor/bin:/product/bin:/apex/com.android.runtime/bin:/apex/com.android.art/bin:/data/adb/ksu/bin:/data/adb/magisk:/data/data/com.termux/files/usr/bin
LD_LIBRARY_PATH=/system/lib64:/system/lib:/vendor/lib64:/vendor/lib:/data/data/com.termux/files/usr/lib
HOME=/data/adb
TMPDIR=/data/local/tmp
TERM=xterm-256color
SHELL=/system/bin/sh
```

Custom environment variables are also supported through the advanced settings panel:

```sh
KEY=value
export KEY=value
```

### Root Script Execution

Scripts can be executed through:

- Normal shell
- Root shell via `su -c`

The default working directory is:

```sh
/data/adb
```

Users can also quickly switch to:

```sh
/data/local/tmp
/sdcard/Download
```

or enter any custom directory.

### Permission Selector

kind BN provides a chmod permission selector inspired by file manager permission dialogs.

Supported permission options:

- Owner read/write/execute
- Group read/write/execute
- Others read/write/execute
- SUID
- SGID
- Sticky bit

Generated chmod modes include examples such as:

```sh
755
777
4755
2755
1777
```

### Full-screen Terminal

The app includes a built-in full-screen terminal-style page.

Terminal features:

- Root or non-root command execution
- Command history output
- Shortcut number keys `1-7`
- Keyboard popup button
- Custom terminal font color
- Custom terminal background color
- Custom terminal font size
- Environment variable injection

> This is a lightweight in-app shell runner, not a full Termux bootstrap/runtime.

### Module Inspection

kind BN can inspect common root module locations, including:

```sh
/data/adb/modules
/data/adb/ksu/modules
```

It also scans for possible KernelSU WebUI resources such as:

```sh
webroot
index.html
webui
```

### LSPosed / Xposed Scan

The app scans common LSPosed/Xposed-related paths:

```sh
/data/adb/lspd
/data/adb/lsposed
/data/misc/apexdata/org.lsposed.manager
```

This helps locate module APKs, scope files, JSON/XML configuration files, and related module traces.

### Script Guard

kind BN includes a basic script protection layer for scripts launched from within the app.

It checks for dangerous patterns such as:

```sh
rm -rf /
rm -rf /system
rm -rf /vendor
dd if=... of=/dev/block/...
mkfs.*
mount ... rw ...
blockdev --setrw
fastboot erase
```

If a dangerous pattern is detected before execution, the app blocks the script and returns a protection message.

> Important: this protection only applies to scripts launched by kind BN.  
> It does not globally intercept every process on the device. For real system-wide protection, a Magisk/KernelSU/LSM/eBPF-level component would be required.

### APK Signing Helper

The signing page provides command templates for:

- Public test signing
- Custom keystore signing
- BNSTR exclusive signing profile

Example:

```sh
keytool -genkeypair -v -keystore custom.jks -alias custom -keyalg RSA -keysize 4096 -validity 10000
apksigner sign --ks custom.jks --ks-key-alias custom target.apk
```

> Private keys should never be hardcoded into the application source code.

### Hidden Easter Egg

Long-pressing the **Sign** tab triggers a root-based browser launch:

```sh
am start -a android.intent.action.VIEW -d 'https://b23.tv/ptzFlAR'
```

## UI Design

kind BN uses a clean white interface with:

- Jetpack Compose
- Material 3
- Animated page transitions
- Glassmorphism-style bottom navigation
- Dynamic blur highlight
- Full-screen terminal layout
- Customizable terminal theme

The UI is designed to feel closer to a professional Android root toolbox rather than a basic demo app.

## Branding

- App name: `kind BN`
- Package name: `bn.bnstr.kind`
- Telegram channel: [https://t.me/BNSTR](https://t.me/BNSTR)

## Build

Clone the project and build with Gradle:

```sh
./gradlew :app:assembleDebug
```

Debug APK output:

```sh
app/build/outputs/apk/debug/app-debug.apk
```

## Requirements

- Android 7.0+
- Root access recommended
- `su` binary for root execution
- KernelSU / Magisk environment recommended for module scanning

## Limitations

- The terminal is a lightweight in-app shell executor, not a full Termux runtime.
- Global process/file-operation protection is not implemented.
- LSPosed and KernelSU scans depend on device-specific paths and root permissions.
- APK signing commands are templates unless the required signing tools and keystores exist on the device/environment.

## Disclaimer

kind BN is intended for advanced Android users, developers, and security researchers.

Use it only on devices you own or have permission to modify.  
Running root commands can permanently damage your system or data if used incorrectly.

The authors are not responsible for damage caused by misuse, unsafe scripts, or unauthorized modifications.

## Credits

This project is inspired by public Android root tooling, shell execution workflows, and open-source Android development practices.

Please respect the licenses of any open-source components, tools, or code referenced or reused in this project.

Telegram: [https://t.me/BNSTR](https://t.me/BNSTR)
```
