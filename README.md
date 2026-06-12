# 🌧️ Prototype Pendeteksi Hujan Berbasis IoT Menggunakan ESP32, DHT22, Water Level Sensor, Blynk, dan Telegram Bot

Muhammad Akhyat Tariq Razan 2309106119
Najwan Wi'am Asroshan 2309106107

## 📖 Deskripsi

Prototype ini merupakan sistem pendeteksi hujan berbasis Internet of Things (IoT) yang menggunakan **ESP32** sebagai mikrokontroler utama, **DHT22** untuk memantau suhu dan kelembapan udara, serta **Water Level Sensor** yang dimanfaatkan sebagai alternatif rain sensor untuk mendeteksi adanya tetesan air hujan.

Sistem dapat melakukan monitoring kondisi lingkungan secara real-time melalui platform **Blynk IoT** dan mengirimkan notifikasi otomatis melalui **Telegram Bot** ketika terdeteksi potensi hujan maupun hujan yang sedang berlangsung.

---

## 🎯 Tujuan Proyek

* Memonitor suhu udara secara real-time.
* Memonitor kelembapan udara secara real-time.
* Mendeteksi potensi hujan berdasarkan kelembapan udara.
* Mendeteksi hujan menggunakan Water Level Sensor sebagai rain sensor alternatif.
* Mengirimkan notifikasi otomatis ke Telegram.
* Menyediakan kontrol manual LED dan buzzer melalui Blynk.
* Mengimplementasikan konsep Internet of Things (IoT) pada sistem monitoring cuaca sederhana.

---

## 🛠️ Komponen Hardware

| No | Komponen           |
| -- | ------------------ |
| 1  | ESP32 DevKit V1    |
| 2  | Sensor DHT22       |
| 3  | Water Level Sensor |
| 4  | LED Hijau          |
| 5  | LED Merah          |
| 6  | Buzzer             |
| 7  | Breadboard         |
| 8  | Kabel Jumper       |
| 9  | Smartphone         |
| 10 | Koneksi WiFi       |

---

## 💻 Software yang Digunakan

* Arduino IDE
* Blynk IoT
* Telegram Bot
* GitHub

---

## 📚 Library Arduino

Install library berikut melalui Library Manager Arduino IDE:

```text
Blynk
DHT Sensor Library
Adafruit Unified Sensor
Universal Telegram Bot
ArduinoJson
WiFi
WiFiClientSecure
```

---

## 🔌 Konfigurasi Pin ESP32

| Komponen           | GPIO    |
| ------------------ | ------- |
| DHT22              | GPIO 4  |
| Water Level Sensor | GPIO 34 |
| LED Hijau          | GPIO 26 |
| LED Merah          | GPIO 27 |
| Buzzer             | GPIO 25 |

> Konfigurasi pin dapat diubah pada bagian `#define` di dalam program.

---

## 📱 Dashboard Blynk

### Datastream

| Nama          | Virtual Pin | Tipe    |
| ------------- | ----------- | ------- |
| Suhu          | V0          | Double  |
| Kelembapan    | V1          | Double  |
| Rain Sensor   | V2          | Integer |
| Status Sistem | V3          | String  |
| LED Hijau     | V4          | Integer |
| LED Merah     | V5          | Integer |
| Buzzer        | V6          | Integer |
| Mode Manual   | V7          | Integer |

---

### Tampilan Dashboard

```text
┌────────────────────┐
│      SUHU          │
│      27.5°C        │
└────────────────────┘

┌────────────────────┐
│   KELEMBAPAN       │
│       85%          │
└────────────────────┘

┌────────────────────┐
│   RAIN SENSOR      │
│       35%          │
└────────────────────┘

┌────────────────────┐
│   STATUS SISTEM    │
│ POTENSI HUJAN      │
└────────────────────┘

Mode Manual
[ ON / OFF ]

LED Hijau
[ ON / OFF ]

LED Merah
[ ON / OFF ]

Buzzer
[ ON / OFF ]
```

---

## 🤖 Telegram Bot

Telegram digunakan sebagai media notifikasi utama.

### Jenis Notifikasi

#### Potensi Hujan

```text
🌥 POTENSI HUJAN TERDETEKSI

🌡 Suhu : 27°C
💧 Kelembapan : 85%
```

---

#### Hujan Terdeteksi

```text
🌧 HUJAN TERDETEKSI

Rain Sensor : 35%
```

---

#### Hujan Deras

```text
🌧🌧 HUJAN DERAS TERDETEKSI

Rain Sensor : 85%
```

---

#### Kondisi Normal

```text
✅ Kondisi kembali NORMAL
```

---

## 🧠 Logika Sistem

### NORMAL

Kondisi:

```text
Kelembapan < 80%
Rain Sensor < 20%
```

Output:

```text
LED Hijau ON
LED Merah OFF
Buzzer OFF
```

---

### POTENSI HUJAN

Kondisi:

```text
Kelembapan ≥ 80%
Rain Sensor < 20%
```

Output:

```text
LED Hijau OFF
LED Merah ON
Buzzer Bunyi Sebentar
```

---

### HUJAN TERDETEKSI

Kondisi:

```text
Rain Sensor ≥ 20%
```

Output:

```text
LED Merah ON
Buzzer ON
```

---

### HUJAN DERAS

Kondisi:

```text
Rain Sensor ≥ 70%
```

Output:

```text
LED Merah ON
Buzzer ON Terus
```

---

## 🔄 Diagram Alur Sistem

```text
          DHT22
             │
             ▼
      Suhu & Kelembapan
             │
             ▼
      Potensi Hujan
             │
             ▼

      Water Level Sensor
     (Rain Sensor Alternatif)
             │
             ▼
      Deteksi Air Hujan
             │
             ▼
            ESP32
        ┌────┴────┐
        ▼         ▼
      Blynk    Telegram
   Monitoring  Notifikasi
        │
        ▼
   LED & Buzzer
```

---

## 🌧️ Cara Kerja Sistem

1. DHT22 membaca suhu dan kelembapan udara.
2. Jika kelembapan mencapai atau melebihi 80%, sistem menetapkan status **Potensi Hujan**.
3. Water Level Sensor digunakan sebagai rain sensor alternatif untuk mendeteksi tetesan air hujan.
4. Ketika sensor terkena air, status berubah menjadi **Hujan Terdeteksi**.
5. Jika intensitas air yang mengenai sensor semakin tinggi, status berubah menjadi **Hujan Deras**.
6. Sistem mengaktifkan LED dan buzzer sesuai kondisi.
7. Notifikasi otomatis dikirim ke Telegram.
8. Data sensor ditampilkan secara real-time pada dashboard Blynk.

---


## 📈 Pengembangan Selanjutnya

* Menambahkan rain sensor khusus.
* Penyimpanan data ke database cloud.
* Menampilkan grafik histori data.
* Integrasi MQTT Protocol.
* Integrasi Machine Learning untuk prediksi cuaca.
* Integrasi panel surya sebagai sumber daya mandiri.

---

## 👨‍💻 Tim Pengembang

**Proyek IoT Pendeteksi Hujan Berbasis ESP32**

Dikembangkan sebagai implementasi pembelajaran:

* Internet of Things (IoT)
* Embedded System
* Monitoring Lingkungan
* Integrasi Cloud dan Telegram Bot

