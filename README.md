# 3522 Bulut_Bilisim_Final_Projeleri
## Proje 3: Akıllı Veri Analitiği ve Makine Öğrenmesi Uygulaması
**Yapılan İşlem:** Ev fiyatlarını tahmin etmek üzere yerel makinede bir makine öğrenmesi modeli geliştirilmiştir.
**Kullanılan Teknolojiler:** Python, Jupyter Notebook, Pandas, Scikit-learn, Joblib.
**Veri Seti:** Evlerin metrekare (SqFt), yatak odası (Bedrooms) ve banyo (Bathrooms) sayılarına göre fiyat (Price) hedefleyen 200 satırlık simüle edilmiş veri seti oluşturulmuş ve `house_prices.csv` adıyla kaydedilmiştir.
**Model Eğitimi:** Scikit-learn kütüphanesinin `RandomForestRegressor` algoritması kullanılarak model eğitilmiş ve başarıyla doğrulanmıştır.
**Çıktı:** Eğitilen model bulut platformuna (AWS S3 & Lambda) yüklenmeye hazır hale getirilerek `ev_fiyat_modeli.joblib` formatında dışarı aktarılmıştır.
