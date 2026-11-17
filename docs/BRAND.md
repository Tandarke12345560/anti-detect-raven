# BRAND.md — Anti-Detect-Raven tasarım dili

Bu kılavuz, "NOKTA" marka kimliği yaklaşımının Anti-Detect-Raven'e uyarlamasıdır: **beş renk, yuvarlak hatlar, sade çizimler**.

## 1. Renk paleti

| Token | Hex | Kullanım |
|---|---|---|
| `--black` | `#000000` | Zemin, birincil yüzey, güçlü kontrast, buton zemini |
| `--ink` | `#272626` | Gövde metni |
| `--teal` | `#15c0cc` | Vurgu, aktif durum, bağlantı, ana eylem |
| `--gray` | `#999b9b` | İkincil metin, ayırıcılar, pasif ikonlar |
| `--green` | `#2ecc59` | Onay, başarı, tamamlanma |

```css
--black:#000000; --ink:#272626; --teal:#15c0cc; --gray:#999b9b; --green:#2ecc59;
```

**Hiyerarşi:** siyah yapı, kömür metin, turkuaz dikkat, yeşil ilerleme, gri ikincil.

### Kullanım oranları
- **Arayüz:** siyah/beyaz taşıyıcı (%70), turkuaz vurgu (%18), gri destek (%8), yeşil onay (%4)
- **Kampanya/banner:** turkuaz öne çıkar, siyah denge kurar, yeşil küçük vurgu

## 2. Tipografi

| Rol | Ağırlık | Not |
|---|---|---|
| Display | 900 | -3% letter-spacing, hero/kampanya |
| Başlık | 700 | -2% letter-spacing |
| Gövde | 400 | 1.6 line-height |
| İtalik | 400 italic | Vurgu, slogan, notlar |
| Etiket | 500 | +14% letter-spacing, UPPERCASE |

Font: **Google Sans** (Roboto yedek). Minimum boyut: 12 px.

## 3. Logo

İç içe iki yuvarlak + geometrik raven silueti: dış halka istikrarı, iç turkuaz nokta odağı temsil eder.

- `assets/logo.svg` — ana (açık zemin)
- `assets/logo-reverse.svg` — koyu zemin (beyaz halka + turkuaz nokta)
- `assets/terminal-logo.svg` — siyah kutu, yeşil `|/|` glyph, beyaz marka adı
- `assets/banner.svg` / `assets/animated-banner.svg` — README hero

**Koruma alanı:** logo yüksekliğinin yarısı kadar boşluk (iç nokta çapı = X). Minimum boyut: 24 px.

## 4. Terminal logosu kuralları

- Kutu rengi: `#000000` (değiştirilmez), köşe yarıçapı 12 px
- Glyph: `|/|` — her zaman `#2ecc59` (yeşil)
- Yazı tipi: monospace (Roboto Mono)
- ASCII banner kullanımında kutu yok — yalnızca siyah terminal zemini

```
+--------------------------------------+
|  |/|  ANTI-DETECT-RAVEN              |
|  iz bırakma, raven gibi uç           |
+--------------------------------------+
```

## 5. Doğru / Yanlış

✓ Onaylı 5 rengi kullan · ✓ yeterli koruma alanı bırak · ✓ koyu zeminde reverse varyant
✗ Gradyan/gölge/efekt ekleme · ✓✗ logoyu döndürme-esnetme · ✗ koruma alanına öğe koyma · ✗ onay dışı renk

## 6. Bileşen dili

- Köşe yarıçapları: 12 / 20 / 32 px, pill etiketler (999 px)
- İkonlar: 24×24 ızgara, 1.7 px stroke, yuvarlak uçlar (`stroke-linecap:round`)
- Progress bar'lar: pill track + dolgu rengi hiyerarşideki gibi (turkuaz aktif, yeşil tamamlandı, siyah birincil, gri pasif)
- Marka sesi: net, sakin, yardımcı. Abartısız. ("Derleme tamamlandı." — değil "Harika! Muhteşem!")
