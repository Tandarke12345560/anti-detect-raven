# BUILD.md — Detaylı derleme kılavuzu

Bu repoyu derlemek için gereken her şey. Test edilen ortam: **instabox `android` template** (Debian 13, x86_64, 4 vCPU / 8 GB RAM + 8 GB swap, JDK 21, Gradle 9.8.1).

## Gereksinimler

- Linux (Ubuntu 22.04+ / Debian 13) — WSL çalışmaz
- JDK 17+ (JDK 21 test edildi), Android SDK + cmdline-tools
- ~25 GB boş disk, 8 GB+ RAM (swap önerilir)
- Python 3.10+ (glean_parser için venv)

## Adımlar

### 1. Klonla

```bash
git clone https://github.com/Tandarke12345560/anti-detect-raven.git
cd anti-detect-raven
```

> **Not:** `android-components` bu repoda **vendor** edilmiştir (submodule değildir). Ekstra `submodule update` adımı yoktur.

### 2. Iceraven patch script'ini çalıştır

```bash
bash automation/iceraven/patch_android_components.sh
```

Bu script şunları yapar: search engine asset'leri kopyalar, search/toolbar/top-sites patch'lerini uygular, version catalog yollarını standalone-layout'a çevirir, crash-reporter kaynaklarını hazırlar ve `netwerk/dns/effective_tld_names.dat` dosyasını indirir (wget gerektirir).

### 3. Python venv + glean_parser

```bash
python3 -m venv venv
venv/bin/pip install "glean_parser~=20.1" pyyaml
venv/bin/python automation/iceraven/toolkit/crashreporter/generate_crash_reporter_sources.py
```

### 4. SDK parçaları

```bash
sdkmanager "ndk;29.0.14206865"
sdkmanager "build-tools;37.0.0" "platforms;android-37.2"
```

(AGP 9.4.1 compileSdk 37.2 ister; NDK sürümü Iceraven CI ile aynıdır.)

### 5. Derle

```bash
export GRADLE_USER_HOME=/data/gradle-home   # cache'i kalıcı/ayrı diske al
export ANDROID_HOME=/opt/android-sdk
export PATH="$PWD/venv/bin:$PATH"           # glean python env
./gradlew app:assembleForkDebug -PversionName=0.1.0-adr
```

İlk derleme 20-40 dk sürer (Maven + GeckoView binary indirmeleri dahil).

### 6. Çıktılar

| APK | Yol |
|---|---|
| arm64 (telefon) | `gradle/build/app/outputs/apk/forkDebug/app-arm64-v8a-forkDebug.apk` |
| x86_64 (emülatör) | `gradle/build/app/outputs/apk/forkDebug/app-x86_64-forkDebug.apk` |
| armv7 (eski cihaz) | `gradle/build/app/outputs/apk/forkDebug/app-armeabi-v7a-forkDebug.apk` |

## Sorun giderme

### `remote unpack failed` / push sorunları
GitHub'a 100 MB'tan büyük dosya push etmeyin; build çıktıları (`gradle/build/`) commit edilmemelidir.

### OOM (8 GB RAM'de)
Derleme sırasında **Android emülatör/container'ı durdurun** ve swap ekleyin:

```bash
docker stop instabox-android          # varsa
sudo fallocate -l 8G /data/swapfile && sudo chmod 600 /data/swapfile
sudo mkswap /data/swapfile && sudo swapon /data/swapfile
```

Gradle JVM'i sınırlayın: `GRADLE_OPTS="-Dorg.gradle.jvmargs=-Xmx3g -XX:MaxMetaspaceSize=1g -Dkotlin.daemon.jvm.options=-Xmx2g"`

### `publicsuffixlist does not exist` / version catalog hataları
Patch script'in çalıştığından emin olun; `android-components/settings.gradle` içindeki catalog yolu `../gradle/libs.versions.toml` olmalı (script bunu otomatik düzeltir).

### `wget: command not found` / `No module named 'yaml'`
```bash
sudo apt-get install -y wget
venv/bin/pip install pyyaml     # ya da script'i venv python ile çalıştırın
```

### x86_64 container'a kurulum
```bash
adb install -r gradle/build/app/outputs/apk/forkDebug/app-x86_64-forkDebug.apk
adb shell am start -n io.github.forkmaintainers.iceraven.debug/org.mozilla.fenix.HomeActivity
```
