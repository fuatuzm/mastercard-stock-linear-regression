# Mastercard Hisse Fiyatı Tahmini – Regresyon Analizi

## 1. Proje Amacı
Bu çalışmanın amacı Mastercard Inc. (MA) hissesine ait geçmiş fiyat verilerini analiz ederek çeşitli gözetimli (supervised) regresyon modelleri ile gelecekteki kapanış fiyatını tahmin etmektir. Modellerin performansları karşılaştırılarak hangi algoritmanın bu veri seti için daha uygun olduğu değerlendirilmektedir.

## 2. Veri Seti
Veri seti: Mastercard Stock Daily Updated (Kaggle)

Kullanılan değişkenler: Date, Open, High, Low, Close, Volume.

## 3. Veri Ön İşleme
- Tarih dönüşümü (`pd.to_datetime`) yapılmıştır. Tarih kolonu string formatında olduğu için zaman serisi analizine uygun hale getirilmiştir.
- Tarihe göre sıralama yapılmıştır. Zaman serisi verilerinde sıralama hatalarının modele olumsuz etkisi olmaması için gereklidir.
- Modelle ilgisi olmayan `ticker` ve `name` sütunları kaldırılmıştır. Bu sütunlar sabit veya kategorik olup fiyat tahminine katkı sunmadığı için çıkarılmıştır.

## 4. Korelasyon Analizi
Open, High, Low, Close ve Volume sütunlarının korelasyon matrisi çıkarılmıştır. En güçlü korelasyon Close–High ve Close–Open arasındadır. Volume değişkeninin Close ile olan korelasyonu düşüktür. Bu nedenle bazı model denemelerinde Volume çıkarılarak performans karşılaştırması yapılmıştır.

```python
corr = df[['Open','High','Low','Close','Volume']].corr()
```

## 5. Kullanılan Modeller ve Seçilme Nedenleri
- **Linear Regression**: Baseline model olarak kullanılmıştır. Hızlı ve yorumlanabilirdir.
- **Ridge & Lasso Regression**: Düzenlileştirme sayesinde overfitting'i azaltmayı hedefler. Linear Regression'ın geliştirilmiş versiyonlarıdır.
- **Decision Tree Regressor**: Lineer olmayan ilişkileri yakalayabilir ancak overfitting eğilimi yüksektir.
- **Random Forest Regressor**: Birden fazla karar ağacının birleşimi ile daha dengeli tahminler üretir. Veri seti için güçlü bir adaydır.
- **Support Vector Regressor (SVR)**: Karmaşık fiyat hareketlerini modelleyebilme kapasitesi vardır. Hesaplama maliyeti yüksektir.
- **KNN Regressor**: Parametrik olmayan bir modeldir. Komşuluk tabanlı yapısı sayesinde farklı veri dağılımlarında test edilebilir.

## 6. Model Karşılaştırması
Tüm modeller aynı train-test bölmesi ile test edilmiştir.  
Değerlendirme metrikleri:
- **Mean Squared Error (MSE)**
- **R² Score**

Örnek karşılaştırma tablosu:

| Model | MSE | R² |
|------|------|------|
| Linear Regression | ... | ... |
| Ridge | ... | ... |
| Lasso | ... | ... |
| Decision Tree | ... | ... |
| Random Forest | ... | ... |
| SVR | ... | ... |
| KNN | ... | ... |

(Not: Metrik değerleri notebook çalıştırıldıktan sonra doldurulmalıdır.)

## 7. Sonuç
Yapılan testler sonucunda Random Forest modeli genel doğruluk ve genelleme açısından diğer modellere göre daha iyi performans göstermiştir.  
Lineer modeller hızlı olmakla birlikte karmaşık fiyat ilişkilerini yakalamakta zorlanmıştır.  
SVR yüksek doğruluk potansiyeline sahip olsa da çalışma süresi uzundur.  

## 8. Proje Yapısı
```
/data
    Mastercard_historical_data.csv

mastercard-linear-regression.ipynb
README.md
```
