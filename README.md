# Burdur Gölü Kıyı Kenar ve Alan Değişimi Analizi (1984–2024)

## Bilgi

- Veriler [EarthExplorer](https://earthexplorer.usgs.gov/) adresinden alınmıştır.
- Verilerin boyutu büyük olduğu için GitHub'a eklenemedi.

## Kaynak Dosya ID'leri:

1. LT05_L1TP_178034_19840716_20200918_02_T1
2. LT05_L1TP_178034_19940728_20200913_02_T1
3. LT05_L1TP_178034_20040723_20200903_02_T1
4. LC08_L1TP_178034_20140703_20200311_02_T1
5. LC08_L1TP_178034_20240730_20240801_02_T1

---

## İlerleme Aşamaları (Metodoloji)

Bu proje kapsamında Burdur Gölü'nün 40 yıllık (1984-2024) kıyı kenar değişimi ArcGIS programı kullanılarak adım adım aşağıdaki işlemlerle analiz edilmiştir:

### Adım 1: Uydu Görüntülerinin İndirilmesi

- USGS EarthExplorer sitesi üzerinden **Landsat 4-5 TM** ve **Landsat 8-9 OLI/TIRS** uydularına ait 30 metre çözünürlüklü "Collection 2 Level 1" verileri indirilmiştir.
- Görüntülerin karşılaştırılabilir olması için bulutsuz (%0 bulutluluk) ve su yüzeyinin/bitki örtüsünün en iyi yansıdığı **Temmuz/Ağustos aylarına** ait görüntüler tercih edilmiştir.

### Adım 2: Veri Ön Hazırlığı

- İndirilen sıkıştırılmış arşiv dosyaları (RAR/ZIP) ilgili yıllara göre adlandırılmış klasörlere (örn. _L1984, L1994_) çıkartılarak ArcMap ortamına aktarılmaya hazır hale getirilmiştir.

### Adım 3: Bant Kompozitlerinin (Kara-Su Ayrımı) Oluşturulması

- Su kütlelerinin sınırlarını net olarak belirlemek ve karayla karışmasını önlemek (özellikle bataklık ve orman ayrımı için) amacıyla **Kara-Su bant kompozitleri** uygulanmıştır.
- **Landsat 8-9 (2014, 2024) için:** 5-6-4 (NIR - SWIR1 - Red) bant kompoziti kullanılmıştır.
- **Landsat 4-5 (1984, 1994, 2004) için:** 4-5-3 (NIR - SWIR1 - Red) bant kompoziti kullanılmıştır.
- Görüntüler bir çalışma sahası sınırı (dörtgen) çizilerek maskelenmiş (clip) ve GeoTIFF formatında dışa aktarılmıştır.

### Adım 4: Kontrollü Sınıflandırma (Supervised Classification)

- Kesilmiş görüntüler üzerinde göl ve kara yüzeylerini ayırt edebilmek için "Interactive Supervised Classification" (Kontrollü Sınıflandırma) yöntemi kullanılmıştır.
- Su ve kara (çıplak yüzey, orman, tarım arazisi vb.) için ayrı ayrı eğitim örneklemleri (training samples) toplanmış ve bu örnekler birleştirilerek görüntü iki ana sınıfa ayrılmıştır.
- Her on yıllık periyot için suyun çekildiği alanlardaki yeni durum dikkate alınarak bu örneklemler güncellenmiş ve sınıflandırılmış görüntüler elde edilmiştir.

### Adım 5: Vektörizasyon (Raster'dan Vektöre Dönüştürme)

- Hücre tabanlı raster görüntülerde doğrudan alan hesabı yapılamadığı için göl yüzeyine (su sınıfına) ait veriler "Raster to Polygon" aracıyla vektör veriye (poligon) dönüştürülmüştür.
- Piksel hassasiyetini korumak ve matematiksel olarak en doğru alan hesabını yapabilmek için dönüşüm esnasında **"Simplify Polygon" (Poligonu Yumuşat) seçeneği kapalı** tutulmuştur.

### Adım 6: Veri Temizliği ve Alan Hesaplama

- Sınıflandırma esnasında su sınıfına dahil olan aykırı alanlar (göletler, ufak barajlar veya hata kaynaklı pikseller) Editor aracı kullanılarak temizlenmiş ve göl tek parça bir poligon haline getirilmiştir.
- Öznitelik tablosu (Attribute Table) üzerinden alan geometrisi hesaplanarak (**Calculate Geometry**) her yıl için göl yüzey alanı kilometrekare (km²) cinsinden bulunmuştur.

### Adım 7: Haritalandırma ve Çıktı Alma

- Layout (Çıktı) ekranına geçilerek beş farklı yılın uydu görüntüleri ve sınıflandırılmış haritaları bir araya getirilmiştir.
- Haritalara kuzey oku, ölçek, başlık ve lejant eklenerek görselleştirmeleri tamamlanmış, sonuçlar Word veya sunumlarda kullanılmak üzere yüksek çözünürlüklü (400 DPI) **PNG** formatında kaydedilmiştir.

---

## Analiz Sonuçları Özeti

Yapılan alan hesaplamaları sonucunda yıllara göre elde edilen Burdur Gölü yüzey alanları şöyledir:

- **1984:** 205,5 km²
- **1994:** 175,2 km²
- **2004:** 158,7 km²
- **2014:** 134,3 km²
- **2024:** 116,4 km²

_Göl, 40 yıllık periyotta çevresel etkiler, kuraklık ve bataklık formasyonuna dönüşüm sebebiyle yaklaşık olarak toplamda 89,1 km² (%43) küçülerek kritik bir seviyeye inmiştir._

![](https://raw.githubusercontent.com/metehanio/burdur-golu-kiyi-kenari-analizi/refs/heads/master/%C3%87%C4%B1kt%C4%B1/K%C4%B1y%C4%B1%20Kenar%20De%C4%9Fi%C5%9Fim%20Analizi%20-%20G%C3%B6l%20-%20Kademe.png)

---

## Rapor

Yapılan tüm bu uzaktan algılama işlemleri, analiz metodolojisi ve elde edilen bulgular detaylı bir şekilde belgelendirilmiştir. Oluşturulan bu belge, proje dizini altındaki **`Rapor`** klasörü içerisinde **"Burdur Gölü Kıyı Kenar ve Alan Değişimi Analizi (1984–2024) Raporu"** ismiyle yer almaktadır.

![[Burdur Gölü Kıyı Kenar ve Alan Değişimi Analizi (1984–2024) Raporu.pdf]]