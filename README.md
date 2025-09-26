# skin-disease-classification

Bu repo, Akbank Derin Öğrenme Bootcamp kapsamında geliştirdiğim deri hastalıkları sınıflandırma projesine aittir.  
Projenin amacı, farklı deri hastalıklarını içeren görsellerden bir CNN tabanlı model ile sınıflandırma yapmaktır.  
Çalışma, Kaggle üzerinde gerçekleştirilmiş ve görseller, eğitim süreci ile metrikler detaylı şekilde raporlanmıştır.  
NOT:Notebook ekran çıktıları teknik aksaklıklardan ötürü kayıt esnasında sıkıntılar çıkarmıştır çok fazla süre kalmadığı için yeniden run edilip çıktılar çok iyi şekilde ortaya koyulamamıştır.

---

## Giriş

Bu projede elimde bulunan **Skin Disease Dataset** kullanılarak görseller üzerinden deri hastalıklarının otomatik sınıflandırılması amaçlanmıştır.  
Dataset, 22 farklı deri hastalığı sınıfı içermektedir (ör. Akne, Egzama, Vitiligo, Lupus, Psoriasis, vb.).  

Çalışma adımları:  
- **EDA (Exploratory Data Analysis)**: Görsel dağılımı, bulanıklık analizi, duplicate temizliği, görsel boyut analizleri  
- **Veri Ön İşleme**: Data augmentation, resizing, temizleme  
- **Modelleme**: CNN tabanlı model + Transfer Learning denemeleri (ResNet50, VGG16)  
- **Değerlendirme**: Accuracy, Loss grafikler, Confusion Matrix, Classification Report, Grad-CAM görselleştirme  

---

## Metrikler

- **CNN Modeli**:  
  - Train Accuracy ≈ %39  
  - Validation Accuracy ≈ %28  
  - Test Accuracy ≈ %32  

- **Transfer Learning (ResNet50)**:  
  - Train Accuracy ≈ %14  
  - Validation Accuracy ≈ %15  
  - Test Accuracy ≈ %18  

- **Hiperparametre Optimizasyonu** (Keras Tuner):  
  - En iyi kombinasyon: conv filters (64–128), kernel (3–5), dense (256), dropout (0.3), optimizer (SGD)  
  - Validation Accuracy ≈ %26  

> Sonuçlar, medikal görsellerin karmaşıklığı ve sınıfların dengesizliği nedeniyle mütevazı kalmıştır.  
> Ancak projenin amacı, **veri temizleme → modelleme → optimizasyon** adımlarını eksiksiz uygulamak olmuştur.  


## Doğruluk Oranlarının Düşük Kalma Sebepleri

Modelin doğruluk oranlarının düşük çıkmasının bazı temel sebepleri şunlardır:

1. **Veri Seti Zorluğu**  
   - 22 farklı sınıf bulunmakta, sınıflar arasında görsel benzerlikler çok fazla.  
   - Rastgele tahmin doğruluğu ≈ %4.5 olduğundan, %30–35 doğruluk aslında baseline’a göre kat kat daha iyi.  

2. **Veri Dengesizliği**  
   - Bazı sınıflarda yüzlerce, bazılarında onlarca görsel bulunuyor.  
   - Bu dengesizlik, modelin az veri olan sınıfları öğrenmesini zorlaştırıyor.  

3. **Veri Kalitesi**  
   - Bulanık ve düşük çözünürlüklü görseller, modelin doğru özellik çıkarmasını engelledi.  
   - Duplicate görseller silinse de tamamen temizlenmesi mümkün olmadı.  

4. **Donmuş Pretrained Modeller**  
   - Kaggle ortamında internet kısıtı nedeniyle ResNet50’nin ImageNet ağırlıkları indirilemedi.  
   - Bu yüzden transfer learning denemeleri beklenen yüksek başarıyı sağlayamadı.  

5. **Kısıtlı Eğitim**  
   - GPU süresi ve kaynak kısıtları nedeniyle epoch sayıları sınırlı tutuldu.  
   - Daha uzun eğitim ve fine-tuning yapılabilseydi doğruluk oranı artabilirdi. 
---

## Ekler

Projede kullanılan önemli adımlar:  
- **Bulanıklık ve Duplicate Temizleme**: Eğitim verisinin kalitesini artırmak için en bulanık ve tekrar eden görseller silinmiştir.  
- **Data Augmentation**: Görsel çeşitliliğini artırmak için rotation, zoom, shift, flip, brightness augmentation uygulanmıştır.  
- **Resizing**: Tüm görseller 224x224 piksel boyutuna indirgenmiştir.  

---

## Sonuç ve Gelecek Çalışmalar

Bu çalışma ile:  
- CNN modeli ve Transfer Learning karşılaştırılmıştır.  
- Hiperparametre optimizasyonu ile model davranışı gözlemlenmiştir.  
- Görsellerin kalitesinin (bulanıklık, boyut farklılıkları, duplicate görseller) sınıflandırma başarısını doğrudan etkilediği görülmüştür.  

📌 Gelecek Çalışmalar:  
- Daha dengeli dataset kullanımı  
- Daha derin modellerin (EfficientNet, DenseNet) fine-tuning ile test edilmesi  
- GPU/TPU üzerinde daha uzun epoch ile eğitim  
- Medikal uzman görüşü ile yanlış sınıflandırmaların incelenmesi  

---

## Linkler

Çalışmamın Kaggle linklerini buradan görebilirsiniz:

- https://www.kaggle.com/code/kymetboyraz/kiymetboyrazderinogrenmenotebook
