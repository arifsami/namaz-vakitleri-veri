# Namaz Vakitleri — Dini Günler Veri Seti

[Namaz Vakitleri Uygulaması](https://github.com/arifsami/003_NamazVakitleriApp) (private repo) için dini günler/geceler verisini barındıran, ayrı ve **public** bir repo. Neden ayrı: uygulamanın kod tabanı private, ama bu veri hassas değil (Diyanet'in kendi public sitesinden) — uygulama bu dosyayı `raw.githubusercontent.com` / jsDelivr üzerinden, herhangi bir kimlik doğrulaması olmadan çeker.

## Güncelleme (her yıl / gerektiğinde)

1. https://vakithesaplama.diyanet.gov.tr/dinigunler.php?yil=YIL adresinden o yılın verisini al.
2. `dini-gunler.json` içindeki `gunler` dizisine yeni yılın kayıtlarını **ekle** (eskileri silmene gerek yok — uygulama zaten "geçti" olanları otomatik ayırıyor, dizi büyüdükçe sorun olmaz).
3. `guncellenmeTarihi` alanını bugüne güncelle.
4. `main`'e push et. Uygulama bir sonraki açılışta (internet varsa) otomatik yeni veriyi çeker ve önbelleğe alır — **yeni bir app store sürümüne gerek yok.**

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
