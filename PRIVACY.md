# Flora Lens Gizlilik Bilgilendirmesi

**Yürürlük tarihi:** 3 Temmuz 2026  
**Uygulama:** Flora Lens Android uygulaması (`com.hmdrn.floralens`)

Bu belge, Flora Lens mobil uygulamasının hangi verileri hangi amaçlarla işlediğini, verilerin nerede tutulduğunu ve kullanıcının hangi kontrolleri kullanabileceğini açıklar.

## Kısa Özet

- Flora Lens kullanıcı hesabı oluşturmaz.
- Yaprak görselleri hastalık analizi için bir sunucuya yüklenmez; yapay zeka modelleri cihaz üzerinde çalışır.
- Teşhis geçmişi yalnız kullanıcı kaydetmeyi seçerse uygulamanın yerel alanında tutulur.
- Yaklaşık konum izni isteğe bağlıdır ve yalnız hava koşullarını yerelleştirmek için kullanılır.
- Uygulamada reklam, davranışsal izleme veya üçüncü taraf analitik SDK'sı bulunmaz.

## İşlenen Veriler

### 1. Kamera ve Galeri Görselleri

Kullanıcı, kamera ile bir yaprak fotoğrafı çekebilir veya Android Photo Picker üzerinden galeriden bir görsel seçebilir.

- Uygulama yalnız kullanıcının çektiği veya sistem seçici üzerinden açıkça seçtiği görsele erişir.
- Görsel, bitki ve hastalık tahmini için cihaz üzerindeki ONNX modelleriyle işlenir.
- Teşhis amacıyla uzak bir sunucuya gönderilmez.
- Analiz sırasında kullanılan geçici kopyalar uygulamanın önbellek alanında tutulabilir ve uygulama veya Android tarafından temizlenebilir.
- Kullanıcı sonucu geçmişe kaydederse görsel, uygulamanın kalıcı özel dosya alanına kopyalanır.

### 2. Teşhis Geçmişi

Kullanıcı bir sonucu geçmişe kaydettiğinde aşağıdaki bilgiler cihazdaki Room veritabanında saklanabilir:

- bitki türü,
- hastalık sınıfı,
- güven değeri veya sonuç durumu,
- teşhis tarihi ve saati,
- cihazdaki yerel görsel yolu.

Bu kayıtlar Flora Lens sunucularına gönderilmez. Kullanıcı kayıtları uygulamadaki **Geçmiş** ekranından silebilir.

### 3. Yaklaşık Konum ve Hava Verisi

Ana ekrandaki çevre koşulları özeti için kullanıcıdan isteğe bağlı yaklaşık konum izni istenebilir.

- İzin verilirse cihazın sağladığı yaklaşık enlem ve boylam, güncel hava verisini almak amacıyla Open-Meteo API'sine gönderilir.
- Flora Lens konum geçmişi oluşturmaz ve yaklaşık konumu kendi veritabanında kalıcı olarak saklamaz.
- Konum izni verilmezse veya konum alınamazsa Ankara için varsayılan koordinatlar kullanılır.
- Hava verisi yalnız bilgilendirme amaçlıdır ve hastalık teşhis modelinin sonucunu değiştirmez.

### 4. Model Katalogu ve Model İndirmeleri

Bitki türüne özgü uzman modeller ihtiyaç halinde Flora Lens model gateway'i üzerinden indirilir.

- İstek sırasında internet hizmetlerinin çalışması için gerekli standart teknik bilgiler, örneğin IP adresi, istek zamanı, istenen dosya ve kullanıcı aracısı altyapı sağlayıcısı tarafından işlenebilir.
- İndirilen model cihazda saklanır ve uygulama tarafından dosya boyutu ile SHA-256 özeti kullanılarak doğrulanır.
- Kullanıcı indirdiği modelleri **Ayarlar** ekranından silebilir.
- Model indirmek için kullanıcı hesabı, ad, e-posta veya telefon numarası istenmez.

## Uygulama İzinleri

| İzin / erişim | Kullanım amacı | Zorunluluk |
| --- | --- | --- |
| Kamera | Uygulama içinden yaprak fotoğrafı çekmek | İsteğe bağlı; galeri kullanılabilir |
| Yaklaşık konum | Yerel çevre koşullarını göstermek | İsteğe bağlı; Ankara verisi kullanılabilir |
| İnternet | Hava verisi, model katalogu ve uzman model indirmeleri | Çevrimiçi özellikler için gerekli |
| Seçilen fotoğraf | Kullanıcının belirlediği görseli analiz etmek | Yalnız seçilen görsel için |

İzinler Android ayarlarından daha sonra geri alınabilir.

## Kullanılan Harici Hizmetler

| Hizmet | Amaç | Paylaşılabilecek teknik veri |
| --- | --- | --- |
| [Open-Meteo](https://open-meteo.com/en/terms) | Güncel hava koşulları | Yaklaşık koordinatlar, IP adresi ve standart istek bilgileri |
| [Cloudflare](https://www.cloudflare.com/privacypolicy/) | Model katalogu, model dosyaları, trafik güvenliği ve hız sınırlama | IP adresi, istek zamanı, istenen yol ve standart ağ kayıtları |
| [GitHub](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement) | APK ve yayın dosyalarının dağıtımı | Kullanıcı GitHub web sayfasını ziyaret ettiğinde GitHub tarafından işlenen web verileri |

Bu hizmetlerin kendi veri işleme ve saklama politikaları geçerlidir. Open-Meteo, ücretsiz API hizmetinin teknik günlüklerinde IP adresi ve coğrafi koordinat bulunabileceğini ve bireysel günlükleri 90 gün sonra sildiğini belirtmektedir.

## Saklama Süreleri ve Silme

| Veri | Saklama yaklaşımı | Kullanıcı kontrolü |
| --- | --- | --- |
| Geçici analiz görseli | Uygulama önbelleğinde geçici | Android veya uygulama tarafından temizlenebilir |
| Kaydedilmiş teşhis ve görsel | Kullanıcı silene, uygulama verileri temizlenene veya uygulama kaldırılana kadar cihazda | Geçmiş ekranından silme |
| İndirilen uzman model | Kullanıcı silene, uygulama verileri temizlenene veya uygulama kaldırılana kadar cihazda | Ayarlar ekranından silme |
| Yaklaşık konum | Flora Lens tarafından kalıcı geçmiş olarak saklanmaz | Konum iznini Android ayarlarından kapatma |
| Sağlayıcı ağ günlükleri | İlgili hizmet sağlayıcının politikasına göre | Sağlayıcının gizlilik kanalları üzerinden |

Android ayarlarından Flora Lens uygulama verilerini temizlemek veya uygulamayı kaldırmak, uygulamanın özel alanındaki teşhis kayıtlarını, kaydedilmiş görselleri ve indirilen modelleri kaldırır.

## Güvenlik Yaklaşımı

- Teşhis çıkarımı cihaz üzerinde gerçekleştirilir.
- Yerel kayıtlar Android'in uygulamaya özel depolama alanında tutulur.
- Model dosyaları indirme tamamlanmadan kalıcı model olarak kullanılmaz.
- İndirilen modeller boyut ve SHA-256 bütünlük kontrollerinden geçirilir.
- Uygulama paketine GitHub erişim anahtarı, R2 kimlik bilgisi veya benzeri kalıcı bir sunucu sırrı eklenmez.

Hiçbir teknik yöntem mutlak güvenlik garantisi vermez; uygulama ve altyapı makul güvenlik önlemleriyle işletilir.

## Kullanıcı Tercihleri

Kullanıcı:

- kamera ve konum izinlerini vermeyebilir veya Android ayarlarından geri alabilir,
- teşhis sonuçlarını geçmişe kaydetmemeyi seçebilir,
- geçmiş kayıtlarını ve ilişkili görselleri silebilir,
- indirilen uzman modelleri kaldırabilir,
- uygulama verilerini temizleyebilir veya uygulamayı kaldırabilir.

## Çocukların Gizliliği

Flora Lens çocuklara yönelik bir hesap veya sosyal hizmet sunmaz ve bilerek çocuklardan kimlik bilgisi toplamaz. Uygulama, kullanıcı hesabı olmadan çalışan bir araştırma ve karar destek prototipidir.

## Değişiklikler

Uygulamanın veri işleme davranışı değişirse bu bilgilendirme güncellenir ve yürürlük tarihi yenilenir. Güncel sürüm bu GitHub deposunda yayımlanır.

## İletişim

Gizlilik veya teknik sorular için [GitHub Issues](https://github.com/Kscl1/flora-lens/issues) üzerinden proje ekibine ulaşabilirsiniz. Issue kayıtları herkese açıktır; kişisel veya hassas bilgi paylaşmayın.

## Kullanım Sınırı

Flora Lens bir araştırma ve karar destek prototipidir. Uygulama sonuçları profesyonel tarımsal teşhis veya danışmanlığın yerine geçmez.
