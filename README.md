
## Pima Indian Diyabet Veri Seti Üzerinde Yapay Sinir Ağı (ANN) Sınıflandırma Projesi

Bu proje, Pima Indian Diyabet Veri Seti'ni kullanarak diyabet durumunu (var/yok) tahmin etmek için geliştirilmiş bir Derin Öğrenme modelinin eğitim ve optimizasyon sürecini detaylandırmaktadır. Modelin aşırı öğrenmeye (overfitting) karşı dayanıklılığını ve genelleme yeteneğini artırmak temel amaçtır.

### 🎯 Proje Amacı ve Çıktıları

1.  **Veri Ön İşleme:** Eksik verilerin (0 değerleri) ele alınması ve tüm özelliklerin standartlaştırılması.
2.  **Düzenlileştirme Teknikleri:** **Dropout** ve **L2 Düzenlileştirme** (Kernel Regularization) kullanarak modelin karmaşıklığının yönetilmesi.
3.  **Optimizasyon:** **Early Stopping** ve **Learning Rate Scheduler** geri çağrımları ile en iyi ağırlıkların bulunması.
4.  **Hiperparametre Araması:** En iyi nöron, batch size ve öğrenme hızı (LR) kombinasyonunu bulmak için manuel Grid Search (rastgele arama) stratejisi uygulanması.
5.  **Detaylı Performans Analizi:** Modellerin **Doğruluk (Accuracy)**, **Kesinlik (Precision)**, **Duyarlılık (Recall)**, **F1-Score** ve **ROC-AUC** değerleri ile karşılaştırılması.

---

### ⚙️ Uygulanan Teknikler ve Sonuçlar

| Metrik | İlk Model (Sadece Dropout) | Dropout + L2 Düzenlileştirme | En İyi Hiperparametre Modeli |
| :--- | :--- | :--- | :--- |
| **Test Doğruluğu (Accuracy)** | %72.92 | %72.40 | **%74.48** |
| **Test Kesinliği (Precision)** | %61.90 | %61.67 | (En İyi LR ve Nöron ile test edilmedi) |
| **Test Duyarlılığı (Recall)** | %58.21 | %55.22 | (En İyi LR ve Nöron ile test edilmedi) |
| **AUC Değeri** | 0.7670 | 0.7584 | (En İyi LR ve Nöron ile test edilmedi) |
| **En İyi Parametreler** | N/A | L2: 0.001 | Nöron: 8, Batch: 32, LR: 0.001 |

#### 🔑 Çıkarımlar

* **Veri Ön İşleme:** Glukoz, Kan Basıncı ve BMI gibi fizyolojik olarak 0 olmaması gereken değerler, veri setinin medyanı ile doldurularak veri kalitesi artırılmıştır.
* **Düzenlileştirme Etkisi:** L2 düzenlileştirmesinin tek başına eklenmesi, bu veri setinde performansı düşürmüştür, bu da modelin zaten sadece Dropout ile iyi bir şekilde düzenlendiğini veya L2 katsayısının (${ \lambda = 0.001 }$) bu problem için ideal olmadığını göstermiştir.
* **Optimizasyon Başarısı:** Manuel rastgele arama ile bulunan parametreler (`Nöron=8, Batch=32, LR=0.001`), tüm denemeler arasında **%74.48** ile en yüksek performansı getirmiştir. Bu, derin öğrenme modelinde mimari seçiminin ve öğrenme hızının düzenlileştirme kadar kritik olduğunu kanıtlamaktadır.

---
