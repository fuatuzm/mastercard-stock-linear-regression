# 📈 Mastercard Stock Price — Linear Regression

Bu proje, Mastercard hisselerinin geçmiş fiyatlarını kullanarak **Linear Regression** modeliyle kapanış fiyatını tahmin etmeyi amaçlar.  
Microsoft'un **ML-For-Beginners** eğitim serisindeki *Linear Regression* dersine benzer şekilde hazırlanmıştır.

## 📊 Kullanılan Veri Seti

Veri seti:  
**Mastercard Historical Data (Kaggle)**  
Günlük açılış, kapanış, hacim ve fiyat bilgilerini içerir.

## 🧪 Yapılan Adımlar

### ✔ 1. Veri Yükleme ve İnceleme
- CSV dosyası okundu  
- İlk 5 satır incelendi  
- Veri tipleri ve eksik değerler kontrol edildi  

### ✔ 2. Tarih Formatı ve Sıralama
- `Date` kolonu `datetime` formatına dönüştürüldü  
- Veri tarih sırasına göre sıralandı  

### ✔ 3. Görselleştirme
- Zaman serisi kapanış fiyatı grafiği çizildi  
- Gerçek vs Tahmin grafiği oluşturuldu  

### ✔ 4. Linear Regression Modeli
Modelde kullanılan bağımsız değişkenler:

- Open  
- High  
- Low  
- Volume  

Tahmin edilen hedef değişken:
- Close (kapanış fiyatı)

Model performans metrikleri:

- **MSE (Mean Squared Error)**  
- **R² Skoru**

## 📷 Örnek Grafikler

### Zaman Serisi Grafik
Notebook içinde otomatik üretilir.

### Gerçek vs Tahmin Grafiği
Notebook içinde otomatik üretilir.

## 📦 Kullanılan Teknolojiler

- Python  
- Pandas  
- Matplotlib  
- Scikit-Learn  
- Jupyter Notebook  

## 🚀 Nasıl Çalıştırılır?

```bash
pip install -r requirements.txt
jupyter notebook
```

Notebook'u açtıktan sonra hücreleri sırayla çalıştırabilirsiniz.

## 📁 Proje Yapısı

```
├── data/
│   └── Mastercard_historical_data.csv
├── mastercard-linear-regression.ipynb
├── README.md
```

## 🎯 Projenin Amacı

Bu proje, finansal veri analizi ve regresyon modellemeyi öğrenmek isteyenler için başlangıç seviyesi bir örnek sunar.  
ML-For-Beginners eğitim serisindeki Linear Regression dersinin gerçek dünya verisiyle uygulanmış versiyonudur.
