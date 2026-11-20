# video-yayin

"Neler Oluyor Şu Hayatta" YouTube kanalındaki videoların Instagram (@neleroluyorsuhayatta) ve TikTok (@neleroluyorsuhayatta) hesaplarına Buffer üzerinden otomatik paylaşımı.

## Nasıl çalışıyor

- `videos/` klasöründeki her video, Instagram ve TikTok için hazırlanmış hâlidir: H.264/AAC, 1080×1920, başında 0,3 saniyelik kapak karesi var. Kapak olarak bu kare seçilir (`thumbnailOffset` = 100 ms).
- `queue.json` yayın sırasını, açıklamaları ve her videonun durumunu tutar:
  - `bekliyor`: henüz Buffer'a eklenmedi
  - `zamanlandi`: Buffer'da Instagram ve TikTok gönderisi planlandı
  - `yayinlandi`: iki gönderi de yayınlandı, video dosyası depodan silindi
- Günde 3 paylaşım yapılır: 12:00, 17:00 ve 21:00 (İstanbul saati).
- Günlük bir zamanlanmış görev her sabah:
  1. Yayınlanan gönderilerin videolarını depodan siler.
  2. Buffer'da bugünden itibaren 3 günlük paylaşım planlı kalacak şekilde sıradaki videoları ekler (ücretsiz planda kanal başına en fazla 10 planlı gönderi olabilir).
  3. `queue.json` dosyasını günceller.

Buffer videoyu `https://raw.githubusercontent.com/bambaskabiricom/video-yayin/main/<dosya>` adresinden çeker. Bu yüzden bir video, iki gönderisi de yayınlanmadan silinmez.
