# Roadmap

## v0.1 — Çalışan sert browser (1-2 hafta)
- Iceraven fork, rebrand (Anti-Detect-Raven), kendi imza + applicationId
- RFP + letterboxing shipped default
- Persona validator + 10-20 Mali-G52 placeholder persona (gerçek cihaz capture'ı bekliyor)
- Basit proxy desteği (profil başına, manual config)

## v0.2 — Profil sistemi (2-4 hafta)
- Multi-process profil (manifest'te `:profileN` process'leri)
- `WebView.setDataDirectorySuffix` benzeri izolasyon → GeckoView'da GeckoRuntime-per-profile
- Profil switcher UI, profil başına persona + proxy + TZ/locale bağlama
- Persona coherence checker: TZ↔proxy geo, locale↔TZ, android_version↔gerçek cihaz

## v0.3 — Engine patch'leri (aylar, isteğe bağlı)
- GeckoView kaynak patch'leri (docs/patches.md Aşama 2)
- Camoufox patch'lerinden mobil-geçerli olanların portu
- Gerçek cihaz capture pipeline (adb script: getprop, GL_RENDERER, UA dump → persona üret)

## Ölçüt: ne zaman "yeterli"?
Kişisel kullanım için v0.2 + gerçek cihaz verili 10-20 persona, yaygın anti-fraud'lara
(sosyal medya web, e-ticaret) karşı yeterli. Cloudflare bot modu / DataDome seviyesi
hedefse v0.3 şart.
