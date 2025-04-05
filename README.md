# TFminiLiDAR Arduino Library

An easy-to-use Arduino library for interfacing the TFmini and TFmini Plus LiDAR sensors via UART using `SoftwareSerial`.

This library simplifies reading distance, signal strength, and internal temperature data from the sensor. Designed for quick integration with ESP32, Arduino Uno, Mega, Nano, and compatible boards.

---

## ✨ Features

- 📏 Reads **distance** in centimeters.
- 📶 Monitors **signal strength** (return quality).
- 🌡️ Reads **internal temperature** in degrees Celsius.
- ⚙️ **Customizable baud rate** from your sketch (default is 115200).
- 🚀 Compatible with **SoftwareSerial** on most boards.
- ✅ Fully tested on **LILYGO T-Eth Lite ESP32**.

---

## 📦 Installation

1. Clone or download this repository.
2. Copy the `TFminiLiDAR` folder to your `Arduino/libraries/` directory.
3. Restart the Arduino IDE.

Alternatively, use the Library Manager once it's published.

---

## 🔌 Wiring

| TFmini Pin | Description      | Arduino Pin (example) |
|------------|------------------|------------------------|
| VCC        | +5V              | 5V                    |
| GND        | Ground           | GND                   |
| TX         | Transmit         | D2 (SoftwareSerial RX)|
| RX         | Receive (optional) | D3 (SoftwareSerial TX)|

> ⚠️ Use voltage level shifting if your board is 3.3V (e.g., ESP32) and your TFmini is 5V.

---

## 🚀 Usage

```cpp
#include <TFminiLiDAR.h>

// RX = D2, TX = D3
TFminiLiDAR tfmini(2, 3);

void setup() {
  Serial.begin(9600);
  tfmini.begin(115200); // Baud rate can be changed if needed
}

void loop() {
  if (tfmini.readData()) {
    Serial.print("Distance: ");
    Serial.print(tfmini.getDistance());
    Serial.print(" cm	");

    Serial.print("Strength: ");
    Serial.print(tfmini.getStrength());
    Serial.print("	");

    Serial.print("Temperature: ");
    Serial.print(tfmini.getTemperature() / 100.0); // in °C
    Serial.println(" °C");
  }
}
```

---

## 📘 API Reference

| Method                   | Description                                  |
|--------------------------|----------------------------------------------|
| `begin(baudRate)`        | Initializes the serial port (default 115200) |
| `readData()`             | Reads and parses the 9-byte data frame       |
| `getDistance()`          | Returns distance in centimeters              |
| `getStrength()`          | Returns signal strength (raw value)          |
| `getTemperature()`       | Returns internal temperature ×100 (divide by 100.0 for °C) |

---

## 🔍 Notes

- The library is based on the 9-byte standard output frame used by TFmini and TFmini Plus in UART mode.
- Temperature is **sensor internal temperature**, not ambient.
- If your TFmini Plus supports command mode, future versions of this library may support additional features like changing output modes, frame rates, or querying firmware versions.

---

## ✅ Tested Hardware

- ✅ LILYGO T-Eth Lite ESP32
- ✅ Arduino Uno/Nano/Mega (using SoftwareSerial)
- ✅ TFmini Plus (UART mode)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 💬 Feedback & Contributions

Feel free to open an issue or pull request if you find bugs or want to suggest new features. You can also email or DM the author with ideas for additional functionality like:
- Firmware version readout
- Command mode support
- I2C variant compatibility
