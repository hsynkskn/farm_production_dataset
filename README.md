Kanada Tarımsal Üretim Verilerinin Analizi ve Üretim Tahmini İçin Makine Öğrenmesi Modeli
1. Giriş
Tarım sektörü, gıda güvenliği, ekonomik kalkınma ve sürdürülebilirlik açısından stratejik bir öneme sahiptir. Bu çalışmada, Kanada'ya ait tarımsal üretim verileri analiz edilerek üretim miktarını tahmin edebilen bir makine öğrenmesi modeli geliştirilmiştir. Araştırma kapsamında, veri ön işleme, keşifsel veri analizi ve Random Forest regresyon algoritması ile modelleme süreçleri sistematik bir şekilde ele alınmıştır. Elde edilen model, yüksek doğrulukla tahminler üreterek tarımsal planlama ve karar destek sistemleri açısından uygulanabilir bir çözüm sunmaktadır.

2. Veri Seti ve Tanımlayıcı Analiz
2.1 Veri Seti Özellikleri
Çalışmada kullanılan veri seti, Kanada’nın çeşitli bölgelerine ait yıllık tarımsal üretim bilgilerini içermektedir. Veri setinde yer alan temel değişkenler aşağıdaki gibidir:

REF_DATE: Referans yılı (zamansal boyut)

GEO: Coğrafi bölge (mekânsal boyut)

Type of crop: Mahsul türü (kategorik değişken)

Average farm price: Ortalama çiftlik fiyatı (ton başına dolar)

Average yield: Ortalama verim (hektar başına kilogram)

Production: Üretim miktarı (metrik ton)

Seeded area: Ekim alanı (hektar)

Total farm value: Toplam çiftlik değeri (dolar)

2.2 Veri Kalitesi Değerlendirmesi
Veri setinin bütünlüğü ve güvenilirliği çeşitli ön işlemlerle değerlendirilmiştir:

Eksik değerler tespit edilmiş ve analiz dışı bırakılmıştır.

Değişken türleri kontrol edilerek uygun veri tipleri atanmıştır.

Aykırı gözlemler tanımlanmış ve istatistiksel yöntemlerle düzeltilmiştir.

3. Veri Ön İşleme ve Özellik Mühendisliği
3.1 Eksik Verilerin İşlenmesi
Veri setindeki eksik gözlemler df.isnull().sum() yöntemiyle tespit edilmiş ve df.dropna() komutu aracılığıyla analiz dışı bırakılmıştır. Bu işlem sırasında veri bütünlüğünün korunmasına özen gösterilmiştir.

3.2 Aykırı Değerlerin Düzenlenmesi
Sayısal değişkenlerdeki aykırı gözlemler, IQR (Interquartile Range) yöntemiyle analiz edilmiştir. Her bir değişken için:

Q1 (25. yüzdelik) ve Q3 (75. yüzdelik) değerleri hesaplanmış,

IQR = Q3 - Q1 formülü uygulanmış,

Aykırı değer sınırları Q1 - 1.5×IQR ve Q3 + 1.5×IQR olarak belirlenmiş,

Belirlenen sınırların dışındaki gözlemler bu değerlere çekilmiştir.

3.3 Kategorik Değişkenlerin Kodlanması
GEO ve Type of crop değişkenleri one-hot encoding yöntemiyle sayısal formata dönüştürülmüştür.

Bu dönüşüm sonrası veri boyutundaki artış dikkatle izlenmiş ve modelin performansına etkisi gözlemlenmiştir.

3.4 Sayısal Değişkenlerin Ölçeklendirilmesi
Tüm sayısal değişkenler, StandardScaler kullanılarak standardize edilmiştir. Böylece değişkenlerin ortalaması 0 ve standart sapması 1 olacak şekilde dönüştürülerek modelin öğrenme süreci optimize edilmiştir.

4. Modelleme Süreci
4.1 Eğitim ve Test Verisi Ayrımı
Veri seti, %80 eğitim ve %20 test olacak şekilde ayrılmıştır. Rastgelelik sabitlenerek (random_state=42), sonuçların tekrarlanabilirliği sağlanmıştır.

4.2 Random Forest Regresyon Modeli
4.2.1 Model Parametreleri
Random Forest regresyon modeli, aşağıdaki başlangıç parametreleriyle yapılandırılmıştır:

n_estimators: 100

max_depth, min_samples_split, min_samples_leaf, max_features: GridSearchCV ile optimize edilmiştir.

4.2.2 Hiperparametre Optimizasyonu
Model parametreleri, GridSearchCV kullanılarak 5 katlı çapraz doğrulama ile optimize edilmiştir. Bu sayede modelin genellenebilirliği artırılmıştır.

4.3 Modelin Değerlendirilmesi
4.3.1 Çapraz Doğrulama Sonuçları
R² Skoru:

Katman bazında: [0.993, 0.992, 0.992, 0.993, 0.992]

Ortalama: 0.9925

Standart sapma: 0.0006

Kök Ortalama Kare Hata (RMSE):

Katman bazında: [44440, 47521, 44895, 43163, 44792]

Ortalama RMSE: 44,962

Standart sapma: 1,420

4.3.2 Performans Analizi
Yüksek R² değeri, modelin üretim miktarını büyük oranda açıklayabildiğini göstermektedir.

Düşük standart sapma, modelin tahminlerinde tutarlı olduğunu kanıtlamaktadır.

RMSE değerleri, üretim büyüklüğü göz önüne alındığında kabul edilebilir seviyededir.

5. Bulgular ve Tartışma
5.1 Modelin Başarımı
Model, tarımsal üretimi yüksek doğrulukla tahmin edebilmekte ve farklı veri alt kümelerinde tutarlı sonuçlar üretmektedir. Ayrıca, aşırı öğrenme (overfitting) belirtileri gözlenmemiştir.

5.2 Önemli Değişkenlerin Etkisi
Seeded area (ekim alanı), üretim miktarını tahmin etmede en önemli değişkendir.

GEO (bölge) değişkeni, bölgesel üretim farklılıklarını yansıtarak tahmin doğruluğunu artırmaktadır.

Type of crop (mahsul türü) üretim üzerindeki önemli etkisiyle modelin açıklayıcı gücünü güçlendirmektedir.

6. Sonuç
Bu çalışmada geliştirilen Random Forest tabanlı makine öğrenmesi modeli, Kanada tarımsal üretim verileri üzerinden yüksek doğrulukla üretim tahmini yapabilmektedir. Model, hem karar vericiler hem de tarım sektörü aktörleri için planlama, kaynak tahsisi, politika geliştirme ve risk yönetimi alanlarında etkili bir karar destek aracı olarak değerlendirilebilir

Veri Kaynağı: Farm Produce Data | 80 years

Notebook: Farm Production Prediction
