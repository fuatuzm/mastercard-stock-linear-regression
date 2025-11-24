# Mastercard Hisse Fiyatı Tahmini – Regresyon Analizi

## 1. Proje Amacı
Bu projenin amacı, Mastercard Inc. (MA) şirketine ait geçmiş hisse fiyatlarını inceleyerek çeşitli gözetimli (supervised) regresyon modelleri ile gelecekteki kapanış fiyatını tahmin etmektir. Çalışmada birden fazla model karşılaştırılmış ve veri setine en uygun tahmin yönteminin belirlenmesi hedeflenmiştir.

---

## 2. Veri Seti
**Kaynak:** Mastercard Stock Daily Updated (Kaggle)

**Kullanılan değişkenler:**  
- *Date*: İşlem tarihi  
- *Open*: Açılış fiyatı  
- *High*: Gün içindeki en yüksek fiyat  
- *Low*: Gün içindeki en düşük fiyat  
- *Close*: Kapanış fiyatı  
- *Volume*: İşlem hacmi  

**Çıkarılan kolonlar:**  
- *ticker* ve *name* sütunları veri setinde sabit olduğundan modele katkı sağlamadığı için kaldırılmıştır.

---

## 3. Veri Üzerinde Yapılan İşlemler ve Nedenleri

### ✔ Tarih Formatı Dönüşümü
`Date` kolonu string formatındaydı.  
Zaman serisi analizi yapılabilmesi için:

```python
df['Date'] = pd.to_datetime(df['Date'])
```

Bu dönüşüm **tarih sıralaması, trend grafiği ve zaman temelli analizler** için gereklidir.

---

### ✔ Tarihe Göre Sıralama
Makine öğrenmesi modelleri sıralanmamış tarih verilerinde hatalı sonuç üretebileceği için veri kronolojik olarak sıralandı.

---

### ✔ Gereksiz Sütunların Çıkarılması
`ticker` ve `name` sabit değerler içerdiği için veri setine **bilgi katmıyor**.  
Bu nedenle modelin gereksiz gürültü almaması için çıkarıldı.

---

## 4. Zaman Serisi Analizi

### **Kapanış Fiyatının Zaman İçindeki Değişimi**
Bu grafik, hissenin yıllar boyunca nasıl bir trend izlediğini görmemizi sağlar.  
Uzun vadeli artış, volatilite dönemleri ve piyasa şokları incelenebilir.

![Kapanış Fiyatı Zaman Serisi](images/gercekvstahmin.png)

---

## 5. Korelasyon Analizi

### **Korelasyon Matrisi**
Modelde kullanılacak değişkenler arasındaki doğrusal ilişkileri gösterir.

![Korelasyon Matrisi](images/korelasyon.png)

### **Analiz Sonuçları**
- **Close–High** ve **Close–Open** arasında güçlü pozitif korelasyon vardır.  
- **Volume**, fiyatla zayıf ilişkiye sahiptir.  
  → Bu nedenle bazı model denemelerinde Volume çıkarılarak performans karşılaştırması yapılmıştır.

---

## 6. Kullanılan Modeller ve Seçilme Nedenleri

Bu projede birden fazla gözetimli regresyon modeli uygulanmıştır:

| Model | Kullanım Nedeni |
|-------|-----------------|
| **Linear Regression** | Basit yapı; başlangıç (baseline) model olarak kullanıldı |
| **Ridge Regression** | Aşırı öğrenmeyi azaltmak için düzenlileştirilmiş lineer yöntem |
| **Lasso Regression** | Gereksiz değişkenleri yok edebilme kapasitesi |
| **Decision Tree** | Doğrusal olmayan ilişkileri yaklayabilmesi |
| **Random Forest** | Birden fazla ağacı birleştirerek yüksek doğruluk sağlar |
| **SVR** | Karmaşık ilişki yapısını modelleyebilir |
| **KNN Regressor** | Veri dağılımına bağlı çalışan parametrik olmayan model |

---

## 7. Model Sonuçlarının Görselleştirilmesi

## 🔮 Tahmini Kapanış Fiyatı (Model Prediction)

Eğitilen Linear Regression modeli kullanılarak, veri setindeki son güne ait veriler üzerinden örnek bir tahmin yapılmıştır.

Modele verilen girdiler:

- Open
- High
- Low
- Volume

Bu değerler kullanılarak modelin ürettiği **tahmini kapanış fiyatı**:

> **≈ 528.79**

Bu sonuç, modelin geçmiş verilere dayanarak gelecekteki fiyatlar hakkında anlamlı tahminler üretebildiğini göstermektedir.


Aşağıdaki grafiklerde her modelin tahmin performansı ayrıca gösterilmiştir.

### **Linear Regression Tahmin Grafiği**
![Linear Regression](images/regression.png)

---



## 8. Sonuç ve Değerlendirme

Bu proje kapsamında Mastercard hissesine ait geçmiş fiyat verileri analiz edilmiş ve çeşitli veri görselleştirmeleri ile fiyat davranışı incelenmiştir. Özellikle kapanış fiyatının zaman içerisindeki eğilimi, değişkenler arası ilişkiler ve model tahmin performansı değerlendirilmiştir.

- Zaman serisi grafiği, hissenin uzun vadede genel olarak yükselen bir trende sahip olduğunu ve belirli dönemlerde yüksek volatilite gösterdiğini ortaya koymuştur.
- Korelasyon analizi sonucunda **Close–High** ve **Close–Open** arasında güçlü pozitif korelasyon tespit edilmiştir. Buna karşılık **Volume** değişkeninin fiyatla zayıf bir ilişkisi olduğu görülmüştür.
- Gerçek değerler ile tahmin sonuçlarının karşılaştırıldığı regresyon grafiği, modelin genel fiyat trendini yakalayabildiğini göstermektedir. Ancak yüksek volatilite dönemlerinde bazı sapmaların oluştuğu gözlemlenmiştir.

**Genel değerlendirme olarak:**  
Bu çalışma, hisse senedi fiyatı gibi karmaşık ve dalgalı veri yapılarında makine öğrenmesi yöntemlerinin temel seviyede başarılı tahminler üretebildiğini göstermektedir. Kullanılan model, fiyat eğilimini genel hatlarıyla yakalasa da volatilite artışının yüksek olduğu dönemlerde tahmin hatalarının arttığı görülmüştür.

Bu nedenle, daha yüksek doğruluk elde etmek için ek özellik mühendisliği, farklı model türlerinin denenmesi veya zaman serisi modellerinin (ARIMA, LSTM vb.) kullanılması gelecekteki çalışmalar için uygun olacaktır.


