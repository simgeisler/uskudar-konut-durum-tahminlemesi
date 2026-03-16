# 🏠 Üsküdar Konut Durumu Tahminleme (Sıfır vs. İkinci El)

Bu proje, İstanbul'un Üsküdar ilçesinde satılığa çıkarılan konutların çeşitli özelliklerini (fiyat, m², bina yaşı, lokasyon vb.) analiz ederek, konutun **"Sıfır" mı yoksa "İkinci El" mi** olduğunu yüksek doğrulukla tahmin etmeyi amaçlayan bir makine öğrenmesi çalışmasıdır.

---

## 📋 Proje Özeti
Gayrimenkul sektöründe konutun durumu, fiyatlandırma ve pazarlama stratejileri için kritik bir parametredir. Bu projede, manuel olarak toplanan veriler üzerinde **Denetimli Öğrenme (Supervised Learning)** yöntemleri uygulanmış ve farklı sınıflandırma algoritmaları performans açısından karşılaştırılmıştır.

- **Veri Kaynağı:** sahibinden.com (Manuel Veri Toplama)  
- **Örneklem Sayısı:** 250 (Başlangıç) → 208 (Temizlik Sonrası)  
- **Hedef Değişken (Label):** `daire_durumu` (1: Sıfır [0-5 yaş], 0: İkinci El [>5 yaş])  
- **Kullanılan Dil ve Kütüphaneler:** Python (Pandas, NumPy, Scikit-Learn, Matplotlib, Seaborn)

---

## 🛠️ Veri Mühendisliği ve Ön İşleme (Data Preprocessing)

### 1. Veri Temizleme (Data Cleaning)
- **Eksik Veri Yönetimi:** %71'i boş olan `aidat` değişkeni veri setinden çıkarıldı. Diğer eksik veriler "En Sık Tekrar Eden (Mode)" değerlerle dolduruldu.  
- **Veri Düzenleme:** `oda_sayisi` (örn: 3+1) → `oda_sayisi_1` ve `salon_sayisi` olarak iki farklı sayısal sütuna bölündü. "Bahçe Katı" gibi metinsel ifadeler numerik değerlere dönüştürüldü; konut dışı türler (Köşk vb.) silindi.  
- **Kategorik Kodlama:**  
  - Binary Encoding: Balkon, asansör, otopark (Var: 1, Yok: 0)  
  - One-Hot Encoding: mahalle değişkeni, semt farklarını modelin anlayabilmesi için dummy değişkenlere dönüştürüldü.

### 2. Aykırı Değer Analizi (Outlier Detection)
- Kutu-Bıyık (Box-Plot) grafikleri kullanılarak fiyat, m², kat sayısı ve banyo sayısı gibi alanlardaki uç değerler temizlendi.  

### 3. Özellik Seçimi (Feature Selection)
- Korelasyon matrisi (heatmap) kullanılarak hedef değişkeni en çok etkileyen ve multicollinearity yaratmayan değişkenler seçildi.
- ![Image](https://github.com/user-attachments/assets/783ccc76-c12c-4744-be43-0881b08fffdd) 
- **Seçilen Özellikler:** `fiyat`, `bina_yasi`, `isitma`, `asansor`, `otopark`.

---

## 🤖 Model Eğitimi ve Algoritmalar
Projede test edilen algoritmalar:  
- **Lojistik Regresyon:** Binary sınıflandırma için olasılık temelli tahmin  
- **Karar Ağaçları (Decision Tree):** Özelliklere göre dallanan akış şeması  
- **Random Forest:** Birden fazla karar ağacının oylama mekanizması  
- Diğer: SVM, Naive Bayes, KNN  

---

## 📊 Performans Değerlendirmesi

| Model               | Doğruluk (Accuracy) | Genel Değerlendirme                   |
|--------------------|------------------|-------------------------------------|
| Lojistik Regresyon  | %94.46           | En dengeli ve başarılı sonuç         |
| Karar Ağaçları      | %94.44           | Çok yakın performans, düşük karmaşıklık |

- **Aşırı Öğrenme Kontrolü:** Eğitim ve test doğruluk farkı < 0.1, modelin genelleyici ve sağlıklı olduğunu gösteriyor.

---


---

## 🎯 Sonuç
Bu çalışma, sınırlı veri seti (208 satır) ile bile **doğru veri ön işleme ve özellik seçimi** teknikleri uygulandığında, gayrimenkul piyasasında %94 civarında yüksek doğrulukla konut segmentasyonu yapılabileceğini göstermektedir.

---

