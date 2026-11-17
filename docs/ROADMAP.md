# ROADMAP.md

## v0.1.0-adr — Baseline ✅ (yayınlandı)

- Iceraven (Fenix/GeckoView) fork'u, `android-components` vendor edildi
- instabox bulut makinesinde derleme pipeline'ı doğrulandı (arm64 / armv7 / x86_64 APK'lar)
- NOKTA tasarım dili: logo, banner, animasyonlu banner, SVG asset seti
- MPL-2.0 lisans, docs, CI

## v0.2 — Profil sistemi

- [ ] `forkDebug` build type'ının rebrand'i: `io.github.antidetectraven` + "Anti-Detect-Raven" adı
- [ ] RFP (`privacy.resistFingerprinting` + letterboxing) shipped default olarak açık
- [ ] GeckoRuntime-per-profile: profil başına izole runtime + cookie deposu
- [ ] Profil switcher UI (ana ekrandan profil ekleme/seçme)
- [ ] Profil başına proxy (HTTP/SOCKS5) + proxy geo ↔ timezone coherence kontrolü
- [ ] Persona validator: `persona.gpu_family` ↔ gerçek `Build.HARDWARE` / `GL_RENDERER` eşleşmesi; uymayan profil kilitlenir
- [ ] Mali-G52 gerçek cihaz persona havuzu (adb ile capture edilmiş gerçek `ro.build.fingerprint`, UA, GL_RENDERER)

## v0.3 — Engine patch'leri (isteğe bağlı, aylık iş)

- [ ] Camoufox patch'lerinden mobil-geçerli olanların GeckoView'a port'u
- [ ] IP-geo tabanlı timezone spoof (RFP'nin UTC sabitlemesini proxy'ye göre esnetme)
- [ ] Canvas noise: engine seviyesinde gerçekçi noise (blank canvas sinyalini azaltmak için)
- [ ] Font listesi: persona'nın device_model'ine uygun subset kısıtlaması
- [ ] Audio stack DSP noise

## Ölçüt / Yeterlilik

Kişisel kullanım için v0.2 + gerçek cihaz verili 10-20 persona, yaygın anti-fraud sistemlerine (sosyal medya web, e-ticaret) karşı yeterli kabul edilir. Cloudflare bot modu / DataDome seviyesi hedefler v0.3 gerektirir.

## Daima

- Her patch sonrası test: CreepJS, bot.sannysoft, FingerprintJS demo, browserleaks
- Baseline karşılaştırması: Iceraven (patch'siz) vs Anti-Detect-Raven (patch'li) çıktı kaydet
