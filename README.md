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


## Proje 4: E-Ticaret ve Auto Scaling Uygulaması

###  Proje Kapsamı ve Amacı
Bu projede, yüksek trafik altında çökmesini engellemek amacıyla otomatik ölçeklendirme (Auto Scaling) altyapısına sahip bir e-ticaret web sunucusu mimarisi kurulmuştur. Sistem, gelen anlık yük durumuna göre sunucu sayısını dinamik olarak artırıp azaltabilmektedir.

###  Kullanılan Teknolojiler
* **İşletim Sistemi:** Ubuntu Server (Linux)
* **Web Sunucusu:** Apache2 (HTTP)
* **Bulut Platformu:** AWS (EC2, AMI, Auto Scaling Groups)

###  Adım Adım Gerçekleştirilen Çalışmalar
1. **Ana Sunucunun Kurulması:** AWS eu-north-1 bölgesinde bir adet Ubuntu EC2 sunucusu ayağa kaldırılmış ve içine Apache2 web sunucusu kurularak temel bir e-ticaret ana sayfası entegre edilmiştir.
2. **Sistem Şablonunun Alınması (AMI):** Sunucunun çalışan kararlı halinin imajı (`E-Ticaret-Sunucu-Kalibi`) alınarak otomasyon sistemine hazır hale getirilmiştir.
3. **Auto Scaling Grubunun Kurulması:** Minimum 1, Maksimum 3 sunucu sınırları belirlenerek bir Auto Scaling Grubu (ASG) yapılandırılmıştır.
4. **Yük Testi ve Ölçeklendirme Simülasyonu:** Sistemde yapay bir yoğunluk simüle edilerek "Desired Capacity" değeri 3'e çıkarılmıştır. AWS, insan müdahalesi olmadan otomatik olarak 2 yeni Ubuntu sunucusunu saniyeler içinde başarıyla devreye almıştır.


## Proje 5: AWS IoT Core ile Akıllı Şehir Trafik Simülasyonu

###  Proje Kapsamı ve Amacı
Bu projede, akıllı şehir vizyonuna uygun olarak Ankara genelindeki kavşakların trafik yoğunluğunu ve araç sayılarını anlık olarak izleyen sanal bir IoT sensör ağı simüle edilmiştir. Cihaz güvenliği ve veri gizliliği AWS IoT sertifikaları ile optimize edilmiştir.

###  Kullanılan Teknolojiler
* **Simülasyon Dili:** Python 3 (Jupyter Notebook ortamı)
* **Protokol:** MQTT (Message Queuing Telemetry Transport)
* **Bulut Platformu:** AWS IoT Core
* **Güvenlik Altyapısı:** X.509 Cihaz Sertifikaları & AWS IoT Policies

###  Adım Adım Gerçekleştirilen Çalışmalar
1. **Sanal Nesne (Thing) Kaydı:** AWS IoT Core üzerinde `Ankara-Trafik-Sensoru` adında sanal bir nesne oluşturulmuş ve cihaza özel X.509 güvenlik sertifikaları ile anahtarlar üretilmiştir.
2. **Güvenlik ve Yetkilendirme (Policy):** Nesnenin `ankara/trafik` konusuna (topic) veri basabilmesi için `iot:*` yetkilerine sahip esnek bir güvenlik politikası tanımlanmıştır.
3. **Python MQTT İstemcisi:** `AWSIoTPythonSDK` kullanılarak sertifikalı bir bağlantı scripti hazırlanmıştır. Kod; Kızılay, Tunalı, Çankaya gibi bölgelerden rastgele ama gerçekçi trafik verilerini (Yoğunluk %, Araç Sayısı) JSON formatında üretmektedir.
4. **Canlı Veri Takibi:** Jupyter üzerinde tetiklenen simülasyon, AWS IoT Core üzerindeki "MQTT Test Client" ekranından anlık olarak doğrulanmış ve verilerin buluta sıfır kayıpla aktığı gözlemlenmiştir.
