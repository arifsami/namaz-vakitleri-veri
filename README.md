# Namaz Vakitleri — Dini Günler Veri Seti

[Namaz Vakitleri Uygulaması](https://github.com/arifsami/003_NamazVakitleriApp) (private repo) için dini günler/geceler verisini barındıran, ayrı ve **public** bir repo. Neden ayrı: uygulamanın kod tabanı private, ama bu veri hassas değil (Diyanet'in kendi public sitesinden) — uygulama bu dosyayı `raw.githubusercontent.com` üzerinden, herhangi bir kimlik doğrulaması olmadan çeker.

**Not (2026-08-22):** İlk denemede jsDelivr CDN kullanıldı, ama gerçek cihazda test edilince purge sonrası bazı edge sunucuların dakikalarca eski veri döndürdüğü gözlemlendi — `raw.githubusercontent.com`'a geçildi (5 dakikalık kısa önbellek, purge gerekmiyor).

## Güncelleme (her yıl / gerektiğinde)

1. https://vakithesaplama.diyanet.gov.tr/dinigunler.php?yil=YIL adresinden o yılın verisini al.
2. `dini-gunler.json` içindeki `gunler` dizisine yeni yılın kayıtlarını **ekle** (eskileri silmene gerek yok — uygulama zaten "geçti" olanları otomatik ayırıyor, dizi büyüdükçe sorun olmaz). **Dikkat:** hicri yıl Miladi'den kısa olduğu için bazı yıllarda aynı kandil (özellikle Miraç/Regaib) tek bir Miladi yıl içinde iki kez düşebilir — böyle bir durumda ikisini de ekle, `id`'leri ay bilgisiyle ayır (örn. `mirac-2027-oca`, `mirac-2027-ara`).
3. `guncellenmeTarihi` alanını bugüne güncelle.
4. `main`'e push et — `raw.githubusercontent.com`'un önbelleği kısa olduğu için genelde birkaç dakika içinde kendiliğinden güncel veriyi vermeye başlar, ekstra bir "purge" adımı gerekmiyor.

Uygulama bir sonraki açılışta (internet varsa) otomatik yeni veriyi çeker ve önbelleğe alır — **yeni bir app store sürümüne gerek yok.**

## Şema

```json
{
  "id": "benzersiz-kisa-id",
  "ad": "Görünen isim",
  "kategori": "kandil | kadir | gunduz | bayram | yilbasi | yemek",
  "hicriTarih": "gösterim metni",
  "baslangic": "YYYY-MM-DD",
  "bitis": "YYYY-MM-DD (tek günlükse baslangic ile aynı)",
  "tarihGosterimi": "kısa gösterim, örn. '20-22 Mart'",
  "kisaAciklama": "liste satırındaki kısa açıklama",
  "detayAciklama": "detay sheet'inde gösterilen uzun açıklama"
}
```

`kategori` alanı uygulamadaki ikon ve "gün/gece" etiketini belirliyor (kandil/kadir → gece + ilgili ikon, diğerleri → gün).
