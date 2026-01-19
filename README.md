🧪 Aşama 1: Simülasyon ve Backend Testleri (Prototype)
Bu modül, donanım entegrasyonuna (CAN Bus bağlantısı) geçmeden önce; MQTT haberleşme altyapısını, sunucu yanıtlarını ve dashboard (arayüz) tasarımını test etmek amacıyla geliştirilmiş Dijital İkiz (Digital Twin) yazılımıdır.

Fiziksel bir araca ihtiyaç duymadan, araçtan gelebilecek verileri (RPM, Hız, Sıcaklık) matematiksel modellerle simüle eder ve karşı taraftan gelen kontrol komutlarını (Kapı Kilitleme, Motor Durdurma) işler.

🎯 Bu Aşamanın Amacı
Güvenli Test Ortamı: Gerçek araç ECU'suna (Elektronik Kontrol Ünitesi) müdahale etmeden önce MQTT protokolünün kararlılığını test etmek.
Dashboard Geliştirme: Donanım sahada değilken bile arayüz geliştiricisine (frontend) anlamlı veri akışı sağlamak.
Çift Yönlü Haberleşme Kontrolü: Sunucudan gelen komutların ESP32 tarafından doğru parse edilip edilmediğini doğrulamak.

⚙️ Simülasyon Mantığı
Yazılım, gerçek sensör verileri yerine aşağıdaki algoritmaları kullanır:
Motor Durumu: Topic: arac/kontrol üzerinden gelen JSON verisi ile motor sanal olarak çalıştırılır (true) veya durdurulur (false).
Dinamik Veri Üretimi: Motor çalıştığı sürece;
Hız: 0-120 km/h arasında lineer artış gösterir.
RPM: Gaz tepkisini simüle edecek şekilde 1000-6000 devir arasında değişir.
Sıcaklık: Motor ısınma eğrisini taklit ederek zamanla yükselir.
Durum Raporlama: Kapı, kilit ve cam durumları hafızada tutulur ve her durum değişikliğinde sunucuya raporlanır.

📊 Kullanılan Teknolojiler
Donanım: ESP32 (Standalone)
Protokol: MQTT (Publish/Subscribe)
Veri Formatı: JSON
