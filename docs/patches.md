# Patch / Yüzey Listesi

Aşama 1 = yalnızca uygulama katmanı + RFP prefs (engine'e dokunma).
Aşama 2 = GeckoView kaynağına persona-aware patch'ler.

## Aşama 1 — prefs + uygulama katmanı (engine patch yok)
- [ ] RFP açıldı: resistFingerprinting + letterboxing (shipped default)
- [ ] Iceraven about:config erişimi korunuyor (debug build'lerde)
- [ ] Persona validator (runtime): persona.gpu_family == gerçek Build/GL_RENDERER ailesi
- [ ] TZ/locale: process seviyesinde override, proxy geo'suyla coherence check
- [ ] Proxy: GeckoRuntime settings üzerinden profile başına HTTP/SOCKS5

## Aşama 2 — GeckoView (Gecko) patch'leri — Camoufox mantığının mobil portu
Sıra önemliden az önemliye; her patch ayrı commit, ayrı feature flag:

1. **Timezone** — IP geo'dan türet (Camoufox'taki mantık). RFP bunu UTC'ye sabitler;
   biz proxy'ye göre set etmeliyiz. (`intl/` init + `Preferences` time zone hook)
2. **Canvas noise** — RFP canvas'ı bloklar (blank döner). "Bloklu canvas" da bir sinyal;
   gerçekçi noise'u engine seviyesinde vermek gerekir (Camoufox `browser/patches`).
3. **Font listesi** — Android font stack zaten cihazdan gelir; persona'nın device_model'ine
   uygun subset'e kısıtla (AOSP/MiUI font farkları gerçekçi kalmalı — aşırı patch gerektirmez)
4. **Screen/density** — RFP letterboxing zaten kırpıyor; persona screen'i ile tutarlı kıl
5. **Audio stack** — DSP noise (aşama 3, düşük öncelik)
6. **Otomasyon/API gizleme** — GeckoView'da Playwright yüzeyi yok, sorun az

## Kural: her patch'ten sonra test
- https://abrahamjuliot.github.io/creepjs/
- https://bot.sannysoft.com/
- https://demo.fingerprint.com/
- https://browserleaks.com/ (canvas, webgl, font, timezone)
Karşılaştırma baseline: Iceraven (patch'siz) vs Anti-Detect-Raven (patch'li) çıktı kaydet.
