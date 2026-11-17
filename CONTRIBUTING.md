# Contributing to Anti-Detect-Raven

Teşekkürler! Katkı kuralları kısa ve net:

## Nasıl katkıda bulunulur

1. Bu repoyu fork'la
2. Bir feature branch aç: `git checkout -b feature/kişilik-adı`
3. Değişikliklerini yap ve commit'le (mesajları Türkçe veya İngilizce, öz yazın)
4. Fork'una push et ve PR aç

## PR şartları

- **Derleme doğrulanmış olmalı:** `./gradlew app:assembleForkDebug` hatasız bitmeli
- Değişiklik, `docs/BRAND.md`'deki tasarım diline (5 renk, yuvarlak hatlar) uymalı
- Engine patch'leri (v0.3): her patch ayrı commit, ayrı feature flag + test çıktısı (CreepJS / bot.sannysoft farkları) PR açıklamasına eklenmeli

## Kod içerikleri

- Uygulama kodu: `app/` (Fenix/Iceraven yapısını korur)
- Motor bileşenleri: `android-components/` (vendor edilmiş; büyük değişiklikler için önce issue aç)
- Persona verileri: `personas/` — **asla gerçek kişisel veri/fingerprint içeremez**; yalnızca gerçek cihazlardan capture edilmiş anonim donanım profilleri

## Davranış kuralları

Saygılı ol, konuya odaklan. Bu araç kişisel gizlilik amaçlıdır; spam/abuse odaklı katkılara kapalıdır.
