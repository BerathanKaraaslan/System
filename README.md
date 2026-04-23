# Otonom Araç Güvenlik Modülü (Safety Corridor Optimizer) 🚗🛡️

Bu proje, otonom araç navigasyon sistemlerinde engel algılama ve çarpışma önleme mekanizmaları için geliştirilmiş, **Destek Vektör Makineleri (SVM - Maksimum Marjin Sınıflandırıcısı)** tabanlı bir güvenlik modülüdür. 

Sensörlerden (Lidar/Kamera) alınan 2 boyutlu engel koordinatlarını işleyerek, otonom aracın geçebileceği en güvenli ve en geniş "güvenlik koridorunu" (Maksimum Marjin) matematiksel olarak hesaplar.

## 🌟 Özellikler

* **Gradient Descent Optimizasyonu:** Standart kütüphaneler yerine, problemi çözmek için Hinge Loss (Menteşe Kaybı) tabanlı özel bir Stochastic Gradient Descent (SGD) algoritması kullanılmıştır.
* **Maksimum Marjin Hesaplaması:** Sınıflandırıcı sadece iki engel grubunu ayıran rastgele bir çizgi bulmaz; aralarındaki dik mesafeyi (güvenlik koridorunu) maksimize eden optimum sınırı bulur.
* **Nesne Yönelimli Mimari (OOP):** Kod yapısı, temiz kod (Clean Code) prensiplerine uygun olarak kapsüllenmiş sınıflardan (Obstacle, SafetyCorridorOptimizer) oluşur.
* **Gerçek Zamanlı Analiz:** Zaman karmaşıklığı doğrusal olan (O(E * N)) bu algoritma, sensör verilerini milisaniyeler içinde işleyerek anlık rotalama sistemlerine entegre edilebilir.

## 📐 Matematiksel Altyapı

Otonom aracın rotasını belirleyen sınır çizgisi şu denklem ile ifade edilir:
w1*x + w2*y + bias = 0

Algoritmanın temel amacı, aşağıdaki optimizasyon problemini çözerek ||w|| değerini minimize etmek ve dolayısıyla koridor genişliğini (2 / ||w||) maksimize etmektir:

1. **Maliyet Fonksiyonu (Hinge Loss):** Engellerin doğru tarafta ve koridorun dışında kalmasını sağlar.
2. **Düzenlileştirme (L2 Penalty):** Sınır çizgisi ile engeller arasındaki hata payını artırarak "over-fitting" (aşırı öğrenme) durumunu engeller ve güvenliği artırır.

## 🚀 Kurulum ve Çalıştırma

Projeyi yerel ortamında çalıştırmak için sisteminde Java 8 veya üzeri bir sürümün yüklü olması gerekmektedir.

1. Depoyu bilgisayarına klonla:
git clone https://github.com/KULLANICI_ADIN/autonomous-safety-corridor.git

2. Proje dizinine git:
cd autonomous-safety-corridor

3. Java dosyasını derle:
javac AutonomousNavSystem.java

4. Simülasyonu başlat:
java AutonomousNavSystem

## 📊 Örnek Çıktı Analizi

Simülasyon çalıştırıldığında, rastgele üretilen çevresel engel verileri işlenir ve konsola aşağıdaki gibi bir analiz raporu basılır:

--- OTONOM ARAÇ GÜVENLİK MODÜLÜ BAŞLATILIYOR ---
Sensör verisi alındı. Toplam engel sayısı: 120

--- OPTİMİZASYON SONUÇLARI ---
Algoritma Çalışma Süresi   : 14 milisaniye
Optimum Ayrıştırıcı Sınır  : -0.3452x + -0.4121y + 4.5120 = 0
Güvenlik Koridoru Genişliği: 3.7214 birim

Not: Bulunan bu sınır, her iki engel grubuna da en uzak mesafede yer alan 'Maksimum Marjin' doğrusudur. 
Bu sayede aracın navigasyon hatalarına karşı en yüksek toleransı (güvenliği) sağlanmıştır.

## 👨‍💻 Geliştirici

**Berathan** *(Yazılım Mühendisliği / Bilgisayar Bilimleri)*
