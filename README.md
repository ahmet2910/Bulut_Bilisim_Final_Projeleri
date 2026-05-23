# 3522 Bulut_Bilisim_Final_Projeleri
## Proje 3: Akıllı Veri Analitiği ve Makine Öğrenmesi Uygulaması
#### 1. Aşama: Yerel Geliştirme ve Model Eğitimi
* **Yapılan İşlem:** Ev fiyatlarını tahmin etmek üzere yerel makinede bir makine öğrenmesi modeli geliştirilmiştir.
* **Kullanılan Teknolojiler:** Python, Jupyter Notebook, Pandas, Scikit-learn, Joblib.
* **Veri Seti:** Evlerin metrekare (SqFt), yatak odası (Bedrooms) ve banyo (Bathrooms) sayılarına göre fiyat (Price) hedefleyen 200 satırlık simüle edilmiş veri seti oluşturulmuş ve `house_prices.csv` adıyla kaydedilmiştir.
* **Model Eğitimi:** Scikit-learn kütüphanesinin `RandomForestRegressor` algoritması kullanılarak model eğitilmiş ve başarıyla doğrulanmıştır.
* **Çıktı:** Eğitilen model bulut platformuna (AWS S3 & Lambda) yüklenmeye hazır hale getirilerek `ev_fiyat_modeli.joblib` formatında dışarı aktarılmıştır.
#### 2. Aşama: Bulut Dağıtımı 
* AWS üzerinde **eu-north-1 (Stockholm)** bölgesinde Python 3.10 tabanlı bir **AWS Lambda** fonksiyonu oluşturulmuştur.
* Projenin bulut ayağında minimum kaynak tüketimi ve maksimum hız hedeflendiği için, modelin veriden öğrendiği ağırlıklar saf Python algoritması olarak serverless fonksiyona entegre edilmiştir. Böylece harici kütüphane bağımlılığı ortadan kaldırılarak sistem optimize edilmiştir.
* Dış dünyadan bu modele veri gönderebilmek amacıyla bir **AWS API Gateway (HTTP API)** tetikleyicisi kurulmuş ve `Open` güvenlik ayarıyla herkesin erişimine açılmıştır.
* Oluşturulan API Endpoint'ine HTTP GET istekleri atılarak sistem test edilmiştir. 
* **Test URL'si:** `https://cc8jmgpjac.execute-api.eu-north-1.amazonaws.com/default/ev-fiyat-tahmin-final`
* **Örnek İstek (50 m², 1 Oda, 1 Banyo):** `https://cc8jmgpjac.execute-api.eu-north-1.amazonaws.com/default/ev-fiyat-tahmin-final?SqFt=50&Bedrooms=1&Bathrooms=1`
* **Dönen JSON Yanıtı:** ```json
  {"Tahmin_Edilen_Fiyat": 830000.0}
