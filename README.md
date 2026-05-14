# ESP32 Marauder — Custom Pin Configuration

> ⚠️ **EDUCATIONAL PURPOSE ONLY**
> This project is intended strictly for educational and learning purposes.
> It must not be used for any malicious, illegal, or unauthorized activities.
> The author is not responsible for any misuse of this project.
> Always obtain proper authorization before testing on any network or device.

---

## 📖 About

This is a personal adaptation of the [ESP32 Marauder](https://github.com/justcallmekoko/ESP32Marauder) project by **justcallmekoko**.

The original project is a suite of WiFi/Bluetooth offensive and defensive tools for the ESP32. This repository contains **only custom pin configurations** adapted for a generic ESP32 Dev Module with a 2.4" ILI9341 TFT display, built as a learning exercise.

All credit for the original firmware goes to [@justcallmekoko](https://github.com/justcallmekoko) and the Marauder contributors.

---

## 🛒 Hardware Used

| Component | Description |
|-----------|-------------|
| ESP32 Dev Module | ESP32-D0WD-V3, dual core 240MHz |
| TFT Display | 2.4" ILI9341 SPI 240x320 with touchscreen and SD slot |

---

## 📌 Wiring — Display → ESP32

| Display Pin | ESP32 Pin | Notes |
|-------------|-----------|-------|
| VCC | 3.3V | Power |
| GND | GND | Ground |
| CS | GPIO 5 | TFT Chip Select |
| RESET | GPIO 4 | TFT Reset |
| DC | GPIO 2 | Data/Command |
| SDI (MOSI) | GPIO 23 | SPI Data |
| SCK | GPIO 18 | SPI Clock |
| LED | 3.3V | Backlight (always on) |

## 📌 Wiring — Touchscreen → ESP32

| Display Pin | ESP32 Pin | Notes |
|-------------|-----------|-------|
| T_CS | GPIO 21 | Touch Chip Select |
| T_CLK | GPIO 18 | Shared with SCK |
| T_DIN | GPIO 23 | Shared with MOSI |
| T_DO | GPIO 19 | Touch MISO |
| T_IRQ | GPIO 27 | Touch Interrupt |

---

## ⚙️ TFT_eSPI User_Setup.h Configuration

```cpp
#define ILI9341_DRIVER

#define TFT_MISO 19
#define TFT_MOSI 23
#define TFT_SCLK 18
#define TFT_CS    5
#define TFT_DC    2
#define TFT_RST   4
#define TFT_BL   32

#define TOUCH_CS 21

#define SPI_FREQUENCY      27000000
#define SPI_READ_FREQUENCY 20000000
#define SPI_TOUCH_FREQUENCY 2500000
```

---

## 🔧 Build Configuration

| Setting | Value |
|---------|-------|
| Arduino Board | ESP32 Dev Module |
| ESP32 Core | 2.0.17 (by Espressif Systems) |
| Partition Scheme | Huge APP (3MB No OTA/1MB SPIFFS) |
| Upload Speed | 921600 |
| Board define | `MARAUDER_V6` |

---

## 📚 Required Libraries

| Library | Author |
|---------|--------|
| TFT_eSPI | Bodmer |
| NimBLE-Arduino | h2zero |
| ArduinoJson | Benoit Blanchon |
| AsyncTCP | dvarrel |
| ESPAsyncWebServer | lacamera |
| EspSoftwareSerial | Dirk Kaar |
| ESP32Ping | marian-craciunescu |
| LinkedList | ivanseidel |

---

## 🐛 Known Fixes Applied

Several source code fixes were required to compile with ESP32 core 2.0.17:

- `EvilPortal.h` — added `static` to `index_html` declaration to fix multiple definition error
- `GpsInterface.cpp` — commented out `HardwareSerial Serial2` declaration (no GPS module used)
- `WiFiScan.cpp` — added `__attribute__((weak))` to `ieee80211_raw_frame_sanity_check` to fix linker conflict
- `WiFiScan.cpp` — replaced `WIFI_AUTH_WPA3_ENTERPRISE` with `WIFI_AUTH_WPA2_ENTERPRISE` (not supported in core 2.0.17)

---

## ⚖️ Legal Disclaimer

This project is a **clone/fork** of ESP32 Marauder, adapted for personal educational use.

- ✅ Use only on networks and devices you own or have explicit permission to test
- ✅ Use for learning about WiFi/Bluetooth security concepts
- ❌ Do NOT use to attack, disrupt, or access networks without authorization
- ❌ Do NOT use for any illegal activities

Unauthorized use of these tools may violate local, national, and international laws.
**Use responsibly and ethically.**

---

## Credits

- Original project: [ESP32 Marauder](https://github.com/justcallmekoko/ESP32Marauder) by [@justcallmekoko](https://github.com/justcallmekoko)
- All firmware logic belongs to the original authors