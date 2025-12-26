# Vehicle-TelemetrySystem
## 📖 Proje Özeti (Abstract)
Bu proje, araç içi haberleşme ağı olan **CAN (Controller Area Network)** veri yolunu dinleyerek (sniffing), araçtan alınan ham verilerin anlamlı bilgilere dönüştürülmesini ve **ESP32** mikrodenetleyicisi aracılığıyla uzaktan izlenmesini sağlayan bir gömülü sistem uygulamasıdır.

Çalışma kapsamında, test aracı (Opel Corsa) üzerinden **500 kbps** hızındaki veri paketleri yakalanmış, **tersine mühendislik** yöntemleri ile araç hızı, motor devri (RPM), motor sıcaklığı gibi kritik parametreler decode edilmiştir. İşlenen veriler, **MQTT** protokolü kullanılarak gerçek zamanlı olarak web arayüzüne aktarılmaktadır.

Bu çalışma, araç filolarının takibi ve kestirimci bakım (predictive maintenance) uygulamaları için bir prototip niteliğindedir.

## 🛠️ Sistem Mimarisi

Sistemin veri akış diyagramı aşağıdadır:

```mermaid
graph LR
A[Araç OBD-II Portu] -- CAN High/Low --> B(CAN Transceiver Modülü)
B -- SPI/UART --> C{ESP32 Mikrodenetleyici}
C -- Veri İşleme & Decoding --> C
C -- WiFi / MQTT --> D[MQTT Broker]
D --> E[Web Arayüzü / Dashboard]

Donanım ve Yazılım Gereksinimleri
Mikrodenetleyici: ESP32 DevKit V1
CAN Arayüzü: MCP2515 CAN Bus Modülü (veya SN65HVD230)
Bağlantı: OBD-II  Kablosu
Güç Kaynağı: Bilgisayar USB bağlantısı

Yazılım & Kütüphaneler
IDE: Visual Studio Code (PlatformIO) veya Arduino IDE
Dil: C++ (Gömülü Yazılım), Python (Veri Analizi için)
Kütüphaneler:
mcp_can.h (CAN iletişimi için)
PubSubClient.h (MQTT haberleşmesi için)
WiFi.h
