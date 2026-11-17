# Derleme — Iceraven → Anti-Detect-Raven

## Gereksinimler
- Linux (Ubuntu 22.04+) veya macOS. **WSL çalışmaz** (Fenix build'i Linux native ister)
- JDK 17, Android SDK (API 34) + build-tools, ~50 GB disk, 16 GB+ RAM
- Android Studio (referans build hataları için)

## Adımlar

```bash
# 1. Iceraven'i fork'la ve klonla
git clone https://github.com/<SEN>/iceraven-browser.git anti-detect-raven
cd anti-detect-raven

# 2. Sürüm tabanını eşle (Iceraven hangi Fenix tag'ine dayanıyorsa, 
#    android-components ve GeckoView sürümünü kilitli tut)
git submodule update --init --recursive   # varsa

# 3. Uygulama kimliğini değiştir
#    app/src/*/AndroidManifest.xml + build.gradle:
#    - applicationId: "org.antidetectraven" (mozilla/iceraven ID'leri KULLANMA — store çakışması)
#    - appName / strings.xml: "Anti-Detect-Raven"
#    - İmza anahtarı üret: keytool -genkeypair (kendi keystore'un)

# 4. Derle
./gradlew assembleArm64        # arm64 (çoğu telefon)
./gradlew assembleArm          # armv7 (eski cihazlar)

# 5. Cihaza kur
adb install app/build/outputs/apk/arm64/debug/*.apk
```

## Notlar
- GeckoView sürümü Gradle dependency'si olarak gelir (`geckoview` artifact). Engine patch'leri için:
  ya `mozilla-central` GeckoView kaynağını submodule yap (ağır yol), ya da v1'de
  **sadece uygulama katmanı + RFP prefs** kullan (hafif yol — önerilen başlangıç).
- RFP'yi açmak için başlangıçta patch'e bile gerek yok:
  `app/src/main/res/xml/`preferences veya first-run prefs:
  `privacy.resistFingerprinting = true`, `privacy.resistFingerprinting.letterboxing = true`
  (Iceraven'de about:config'ten de açılır ama shipped defaults daha güvenli).
