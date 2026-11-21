# arp-scan — Fully Static Build

**Languages:** [English](#english) | [简体中文](#简体中文) | [繁體中文](#繁體中文)

---

## English

A standalone, fully static build of **arp-scan**, a ARP scanning and fingerprinting tool, for four Linux architectures, bundled with the upstream source code. The executables have no dynamic interpreter and no shared-library dependencies, so they run directly on Android phones, embedded devices, and minimal Linux systems.

### Executables

| File | Size | MD5 |
|---|---:|---|
| arp-scan-linux-arm64 | 473,208 B | `e5b8cfced5a7dd14b45804ed6b1777f6` |
| arp-scan-linux-armhf | 461,856 B | `046603f9055a3a0f2df26524023160f2` |
| arp-scan-linux-x64 | 502,160 B | `5d4b52a8a5ed7ddb9938838e4615afc1` |
| arp-scan-linux-x86 | 476,536 B | `b54e794d14e392ef28abb722df9debc3` |

### Static verification

```bash
llvm-readelf -l <binary> | grep -c INTERP   # 0
llvm-readelf -d <binary> | grep -c NEEDED   # 0
llvm-readelf -l <binary> | awk '/LOAD/{print $NF}' | sort -u   # 0x4000
```

All binaries report `INTERP=0`, `NEEDED=0`, and `LOAD align=0x4000` — musl static executables.

### Install and run

```bash
# Linux
install -m755 arp-scan-linux-x64 /usr/local/bin/arp-scan
arp-scan --help

# Android (via adb)
adb push arp-scan-linux-arm64 /data/local/tmp/arp-scan
adb shell "chmod 755 /data/local/tmp/arp-scan"
adb shell "/data/local/tmp/arp-scan --help"
```

### Repository layout

```
bins/   Executables for linux-x64/x86/arm64/armhf
src/    Upstream source: arp-scan-1.10.0.tar.gz
share/  Bundled runtime data files
```

### Offline build

The source is included under `src/` for fully offline reproduction, using the zig toolchain (musl cross-compilation):

```bash
tar xf <source archive> && cd <source dir>
CC="zig cc -target x86_64-linux-musl -static" ./configure --host=x86_64-linux-musl --disable-shared --enable-static
make -j4
```

Architecture triples:

| Target | Linux triple |
|---|---|
| x64 | x86_64-linux-musl |
| x86 | x86-linux-musl |
| arm64 | aarch64-linux-musl |
| armhf | arm-linux-musleabihf |

### Known limitations

- A small number of sub-features that rely on host tools may be unavailable on very restricted systems.

---

## 简体中文

**arp-scan** 的独立全静态构建包，ARP 扫描与指纹识别工具，覆盖四个 Linux 架构，并附上游源码。可执行文件无动态解释器、无共享库依赖，可直接在安卓手机、嵌入式设备和精简 Linux 系统上运行。

### 可执行文件

| 文件 | 体积 | MD5 |
|---|---:|---|
| arp-scan-linux-arm64 | 473,208 B | `e5b8cfced5a7dd14b45804ed6b1777f6` |
| arp-scan-linux-armhf | 461,856 B | `046603f9055a3a0f2df26524023160f2` |
| arp-scan-linux-x64 | 502,160 B | `5d4b52a8a5ed7ddb9938838e4615afc1` |
| arp-scan-linux-x86 | 476,536 B | `b54e794d14e392ef28abb722df9debc3` |

### 静态性核验

```bash
llvm-readelf -l <二进制> | grep -c INTERP   # 0
llvm-readelf -d <二进制> | grep -c NEEDED   # 0
llvm-readelf -l <二进制> | awk '/LOAD/{print $NF}' | sort -u   # 0x4000
```

全部为 `INTERP=0`、`NEEDED=0`、`LOAD align=0x4000`：musl 静态可执行文件。

### 安装与运行

```bash
# Linux
install -m755 arp-scan-linux-x64 /usr/local/bin/arp-scan
arp-scan --help

# Android（通过 adb）
adb push arp-scan-linux-arm64 /data/local/tmp/arp-scan
adb shell "chmod 755 /data/local/tmp/arp-scan"
adb shell "/data/local/tmp/arp-scan --help"
```

### 仓库结构

```
bins/   四个可执行文件（linux-x64/x86/arm64/armhf）
src/    上游源码：arp-scan-1.10.0.tar.gz
share/  附带的运行时数据文件
```

### 离线编译

源码位于 `src/`，可完全离线复现，工具链使用 zig（musl 交叉编译）：

```bash
tar xf <源码包> && cd <源码目录>
CC="zig cc -target x86_64-linux-musl -static" ./configure --host=x86_64-linux-musl --disable-shared --enable-static
make -j4
```

架构 triple：

| 目标 | Linux triple |
|---|---|
| x64 | x86_64-linux-musl |
| x86 | x86-linux-musl |
| arm64 | aarch64-linux-musl |
| armhf | arm-linux-musleabihf |

### 已知限制

- 在受限严重的系统上，个别依赖宿主工具的子功能可能不可用。

---

## 繁體中文

**arp-scan** 的獨立全靜態建構包，ARP 掃描與指紋辨識工具，涵蓋四個 Linux 架構，並附上游原始碼。可執行檔無動態直譯器、無共用程式庫相依性，可直接在安卓手機、嵌入式裝置和精簡 Linux 系統上執行。

### 可執行檔

| 檔案 | 體積 | MD5 |
|---|---:|---|
| arp-scan-linux-arm64 | 473,208 B | `e5b8cfced5a7dd14b45804ed6b1777f6` |
| arp-scan-linux-armhf | 461,856 B | `046603f9055a3a0f2df26524023160f2` |
| arp-scan-linux-x64 | 502,160 B | `5d4b52a8a5ed7ddb9938838e4615afc1` |
| arp-scan-linux-x86 | 476,536 B | `b54e794d14e392ef28abb722df9debc3` |

### 靜態性核驗

```bash
llvm-readelf -l <可執行檔> | grep -c INTERP   # 0
llvm-readelf -d <可執行檔> | grep -c NEEDED   # 0
llvm-readelf -l <可執行檔> | awk '/LOAD/{print $NF}' | sort -u   # 0x4000
```

全部為 `INTERP=0`、`NEEDED=0`、`LOAD align=0x4000`：musl 靜態可執行檔。

### 安裝與執行

```bash
# Linux
install -m755 arp-scan-linux-x64 /usr/local/bin/arp-scan
arp-scan --help

# Android（透過 adb）
adb push arp-scan-linux-arm64 /data/local/tmp/arp-scan
adb shell "chmod 755 /data/local/tmp/arp-scan"
adb shell "/data/local/tmp/arp-scan --help"
```

### 倉庫結構

```
bins/   四個可執行檔（linux-x64/x86/arm64/armhf）
src/    上游原始碼：arp-scan-1.10.0.tar.gz
share/  附帶的執行階段資料檔案
```

### 離線建構

原始碼位於 `src/`，可完全離線重現，工具鏈使用 zig（musl 交叉編譯）：

```bash
tar xf <原始碼封存> && cd <原始碼目錄>
CC="zig cc -target x86_64-linux-musl -static" ./configure --host=x86_64-linux-musl --disable-shared --enable-static
make -j4
```

架構 triple：

| 目標 | Linux triple |
|---|---|
| x64 | x86_64-linux-musl |
| x86 | x86-linux-musl |
| arm64 | aarch64-linux-musl |
| armhf | arm-linux-musleabihf |

### 已知限制

- 在受限嚴重的系統上，個別依賴宿主工具的子功能可能無法使用。
