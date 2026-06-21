# Reference içerik — applixus.com

> `ctx_fetch_and_index` + `ctx_search` ile https://www.applixus.com (anasayfa) ve
> https://www.applixus.com/apps.html (uygulamalar) sayfalarından çıkarıldı.
> Rebuild bu yapıyı ve metinleri esas alır; görsel sadakat için `../screenshots/` kullanılır.

## Genel
- **Dil:** Türkçe.
- **Marka:** Applixus — "Mobil & Web Çözümleri", 2023 kurulu teknoloji şirketi (Gebze/GOSB Teknokent).
- **Sayfalar:** `index.html` (anasayfa, tek sayfa / anchor bölümler) + `apps.html` (uygulamalar).
- **Logo:** `assets/img/logo.webp`.

## Anasayfa (index.html)

### Head / SEO
- `<title>`: **Applixus | Mobil & Web Çözümleri**

### Navigation (header)
- Logo (Applixus) + menü. Menü bölümlere anchor: Hakkımızda (`#about`), Değerler (`#values`), Uygulamalar (`apps.html`), İletişim/İletişime Geç.
- "Görüşme Planlayın" / "Hemen Başlayın" tarzı birincil CTA.

### Hero
- Eyebrow: **APPLIXUS — MOBİL & WEB ÇÖZÜMLERİ**
- **H1:** Applixus inovasyon ve teknolojiyle size hizmet sunuyor
- Alt başlık: "Her işimizi tutkuyla ve özenle yapıyoruz, sizi daha iyi anlamak ve özel çözümler sunmak için buradayız."
- CTA'lar: **Hemen Başlayın** → `#about` · **Uygulamalarımız** → `apps.html`
- İstatistik rozetleri: **5+** Kurumsal Referans · **20+** Yayında Uygulama · **2023**'ten Beri
- Hero görseli + floating etiketler: "iOS, Android & Web", "Yenilikçi Çözümler", "Güvenlik & Gizlilik", "Yapay Zeka Deneyimi".

### Biz Kimiz (#about)
- Başlık: **Biz Kimiz**
- Metin: "Applixus, 2023 yılında kurulmuş bir teknoloji şirketidir. Misyonumuz, müşterilerimize son teknoloji ürünler ve hizmetler sunarak işlerini büyütmelerine yardımcı olmaktır." + müşteri odaklılık/inovasyon vurgulu paragraf.
- Görsel: `assets/img/about.webp` · CTA: **Devam Et** → `#values`
- Üç kart:
  - **01 — İlerlemenin Öncüsü:** sürekli teknolojik inovasyon, yenilikçi çözüm tutkusu.
  - **02 — Sizin İçin Varız:** müşteri önceliği, özel çözüm, başarı desteği.
  - **03 — Mükemmeliyet Standardı:** yüksek kalite ve güvenilirlik standardı.

### Değerlerimiz (#values)
- Değer başlıkları: **Kullanıcı Odaklılık · Sürekli İnovasyon · Güvenlik ve Gizlilik · Veri Etiği · Çevresel Sorumluluk · Müşteri İlişkileri · Yapay Zeka Deneyimi**.

### Geliştirme İlkeleri
- Başlık: **Applixus Mobil & Web Uygulama Geliştirme İlkeleri**
- Kartlar:
  - **Kullanıcı Deneyimi Mükemmeliyeti** — arayüz tasarımından kullanılabilirlik testlerine UX önceliği.
  - **Çapraz Platform Uyumlu** — iOS, Android ve web'de sorunsuz çalışan uygulamalar.
  - **Veri Güvenliği ve Gizliliği** — kullanıcı verisi koruması, en yüksek standartlar.
  - **Hızlı ve Güvenilir Performans** — performans odaklı UX.
  - **Sürekli İnovasyon ve Güncellemeler** — teknolojiye ayak uyduran güncellemeler.
  - **Kullanıcı Geri Bildirimine Açık** — geri bildirimle sürekli iyileştirme.

### Kurumsal Referanslar (logolar)
- Müşteri logoları: **İpragaz · Azercell · Julvera** (+ "5+ Kurumsal Referans"). Her birinde kısa işbirliği açıklaması (ör. Azercell — Azerbaycan telekom; mobil uygulama geliştirme).

### SSS / İletişim bilgisi (FAQ tonu)
- "Kendi ürünleriniz var mı?" → **GoEventX** (kurumsal etkinlik yönetimi), **GoActiveX** (çalışan aktivite takibi), **SMS Shield** (yapay zeka destekli SMS fraud koruması), **Identity Resolution** (müşteri kimlik çözümleme) web ürünleri + Google Play & App Store'da **20+** yayında mobil uygulama.
- "Sizinle nasıl iletişime geçebilirim?" → **info@applixus.com** · **0 (216) 444 98 66** · "Görüşme Planlayın" butonu (çevrim içi görüşme). Çalışma saatleri: hafta içi **09:00 – 18:00**.
- "Ofisiniz nerede?" → **GOSB Teknokent No: 507/9 Z01, Gebze** (Kocaeli).

### Footer
- Marka + kısa açıklama, hızlı bağlantılar (Hakkımızda / Değerler / Uygulamalar / İletişim), iletişim (info@applixus.com, telefon, adres), telif: © Applixus.

## Uygulamalar sayfası (apps.html)

### Head / SEO
- `<title>`: **Uygulamalarımız | Applixus**

### Yapı
- Kart grid'i; her kart: ikon/görsel, başlık, açıklama, **Teknolojiler** etiketleri, **Öne Çıkan Özellikler**, store/web linkleri (Google Play / App Store / web). Bazı kartlarda "Web" rozeti (web ürünleri).

### Web ürünleri
- **SMS Shield — Yapay Zeka ile SMS Koruması** — Python, FastAPI, Özel AI Modeli, Redis, PostgreSQL, React. Gerçek zamanlı risk skorlama, kural motoru, ML tespiti, LLM ikinci görüş, Shadow/Enforce modu, yönetim paneli, Java SDK.
- **Identity Resolution — Müşteri Kimlik Çözümleme** — Python, Özel AI, FastAPI, PostgreSQL, React. Probabilistik eşleştirme, profil birleştirme, adres/hane analizi, küme yönetim paneli.
- **GoEventX — Kurumsal Etkinlik** — Flutter, Firebase, Google Maps API, Spring Boot, real-time bildirim. Etkinlik yönetimi, katılımcı takibi, giriş-çıkış, interaktif harita. (Play + App Store + goeventx.com)
- **GoActiveX** — çalışan aktivite takibi (web).

### Mobil uygulamalar (20+, öne çıkanlar)
- **RingReady: Nail Editor AI** — Flutter, AI Image Processing, CoreML.
- **Lixus: Alışveriş Listesi** — React Native, Firebase, Cloud Firestore.
- **Daily Tarot Cards & Readings** — tarot/falı.
- **Namaz Vakti** — Flutter, GPS, Compass, Local Notifications; ezan saatleri, kıble pusulası, 250+ ülke.
- **Frieren Anime Wallpapers 4K** — Flutter; 4K duvar kağıdı.
- **Learn Spring Boot** — Flutter, SQLite; backend öğrenme.
- **İndirim Radarı** — indirim takip.
- **Bebek Uyku & Rahatlama Sesleri** — Flutter, Audio, Background Services; beyaz gürültü, ninni.
- **Who Told It: Dixit Kart Oyunu** — Flutter, Firebase Realtime DB, WebSocket; gerçek zamanlı multiplayer.
- (+ diğer yayında uygulamalar — toplam 20+.)

### Footer
- Anasayfa ile aynı footer yapısı (marka, linkler, iletişim, telif).

## Rebuild notları
- İki sayfa üret: `index.html` (anasayfa) + `apps.html` (uygulamalar), ortak `assets/styles.css` + `assets/app.js`, paylaşılan header/footer.
- Anchor navigasyon (`#about`, `#values`, vb.) anasayfada çalışmalı; `apps.html` linki anasayfadan uygulamalara gitmeli.
- Görseller harici indirilmez → CSS/placeholder/SVG ile referans yapıyı sadakatle taklit et (logo, hero görseli, uygulama ikonları).
- İletişim bilgileri (e-posta, telefon, adres, çalışma saatleri) birebir korunur.
