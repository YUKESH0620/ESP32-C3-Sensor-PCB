# ESP32-C3 Smart Sensor Board

This repository contains the complete **hardware design** of a custom **ESP32-C3 based Smart Sensor Board**, including schematics, PCB layout, and documentation.

The design integrates **robust power management, multiple sensors, data storage, USB connectivity, and auto-programming**, making it suitable for **IoT, data logging, and embedded systems development**.

---

## 📷 Board Images

### 🔹 Complete Schematic
<img width="1088" height="743" alt="Screenshot 2025-12-26 085358" src="https://github.com/user-attachments/assets/139b2c3f-3f78-4285-b7aa-e1a6b495b93f" />

<img width="1087" height="749" alt="Screenshot 2025-12-26 085602" src="https://github.com/user-attachments/assets/ad2c5c3b-8f81-4bdc-80f2-c4d637b10573" />

<img width="1093" height="750" alt="Screenshot 2025-12-26 085631" src="https://github.com/user-attachments/assets/700ccf38-4650-4adc-b929-a8d74144fca3" />

<img width="1084" height="751" alt="Screenshot 2025-12-26 085659" src="https://github.com/user-attachments/assets/84a88581-1efc-4c0e-8398-ec9f2b19b646" />


### 🔹 PCB Layout
<img width="1919" height="1018" alt="Screenshot 2025-12-26 085844" src="https://github.com/user-attachments/assets/3b8bd616-fbb5-4005-82f5-66c51a86853e" />

### 🔹 3D Views
<img width="1710" height="815" alt="Screenshot 2025-12-26 091250" src="https://github.com/user-attachments/assets/e0156908-8d53-4e83-8612-2a50d07ac91e" />

<img width="1722" height="893" alt="Screenshot 2025-12-26 091325" src="https://github.com/user-attachments/assets/6a486c39-1ce4-4b16-bb1d-7a4ccb0229d6" />

<img width="1725" height="888" alt="Screenshot 2025-12-26 091427" src="https://github.com/user-attachments/assets/8884dd4e-83b2-4330-b871-7ccaa7adb4af" />


---

## 🧠 System Architecture

### Functional Block Diagram
```text
USB-C / Li-Po Battery
│
MCP73831 Charger
│
+5V Rail
│
LM1117-3.3 LDO
│
+3.3V Rail
│
ESP32-C3 MCU
│ │ │ │
│ │ │ Microphone + MAX4466
│ │ BME280 (I2C)
│ LDR (ADC)
SD Card (SPI)
|
SPI Flash
```
---

## ✨ Key Features

### 🔌 Power & Charging
- USB Type-C connector
- Li-Po charging using **MCP73831**
- JST battery connector
- LM1117-3.3 LDO regulator
- Power status LED

### 🧠 Microcontroller
- **ESP32-C3-WROOM-02**
- RISC-V core
- Wi-Fi + BLE
- USB-UART programmable

### 📡 Sensors
- **BME280** – Temperature, humidity, pressure
- **Electret microphone + MAX4466 amplifier**
- **LDR photo sensor**

### 💾 Storage
- SPI Flash memory (W25Q32)
- Micro SD card module (SPI)

### 🔄 Programming & Debug
- CP2102N USB-to-UART
- Auto-programming (DTR/RTS → EN/BOOT)
- Boot & Reset buttons
- Test points

---

## ⚙️ Working Principle

### Power Section
- USB-C provides 5V
- MCP73831 safely charges Li-Po battery
- LM1117 converts 5V to regulated 3.3V
- Decoupling capacitors ensure stable rails

### MCU & Sensors
- ESP32-C3 communicates with:
  - BME280 via I²C
  - SD card & Flash via SPI
  - Microphone and LDR via ADC
- Data can be logged or transmitted wirelessly

### Programming
- USB-C → CP2102N
- DTR/RTS control BOOT & EN automatically
- Compatible with ESP-IDF and Arduino

---

## 🧾 Bill of Materials (Detailed – With Values)

### 🔹 Active Components

| Ref | Component | Value / Part |
|----|----------|-------------|
| U1 | ESP32 MCU | ESP32-C3-WROOM-02 |
| U2 | Env Sensor | BME280 |
| U3 | USB-UART | CP2102N |
| U4 | Charger IC | MCP73831 |
| U5 | LDO Regulator | LM1117-3.3 |
| U6 | SPI Flash | W25Q32 |
| U7 | Mic Amplifier | MAX4466 |
| J1 | USB Connector | USB Type-C |
| J2 | Battery Connector | JST-PH-2 |
| J3 | SD Card Socket | SPI SD |

---

### 🔹 Resistors (From Schematic)

| Ref | Value | Purpose |
|----|------|--------|
| R1 | 10kΩ | MCP73831 PROG |
| R2 | 10kΩ | MCP73831 PROG |
| R3 | 5.1kΩ | USB-C CC pull-down |
| R4 | 5.1kΩ | USB-C CC pull-down |
| R5 | 2kΩ | MCP73831 status |
| R6 | 20kΩ | MCP73831 status |
| R7 | 470Ω | Charging LED |
| R8 | 470Ω | Charged LED |
| R9 | 470Ω | Fault LED |
| R10 | 470Ω | Power LED |
| R11 | 1kΩ | USB VBUS link |
| R12 | 22.1kΩ | USB detection |
| R13 | 47.5kΩ | USB detection |
| R23 | 10kΩ | LDR voltage divider |
| R24 | 4.7kΩ | I²C pull-up |
| R25 | 4.7kΩ | I²C pull-up |
| R26 | 2kΩ | Mic bias |
| R27 | 1MΩ | Mic amp gain |
| R28 | 2kΩ | Mic bias |
| R29 | 1MΩ | Mic amp gain |
| R30 | 10kΩ | Mic amp |
| R31 | 100kΩ | Mic feedback |
| R32 | 10kΩ | Reset pull-up |
| R33 | 10kΩ | DTR control |
| R34 | 10kΩ | RTS control |

---

### 🔹 Capacitors (From Schematic)

| Ref | Value | Purpose |
|----|------|--------|
| C1 | 0.1µF | USB decoupling |
| C2 | 0.1µF | LDO input |
| C3 | 10µF | LDO bulk |
| C4 | 10µF | LDO output |
| C5 | 0.1µF | LDO output |
| C6 | 1µF | MCP73831 |
| C7 | 10µF | ESP32 supply |
| C8 | 0.1µF | ESP32 decoupling |
| C10 | 0.1µF | Sensor decoupling |
| C14 | 0.1µF | Flash decoupling |
| C15 | 0.1µF | BME280 |
| C17 | 10nF | Mic coupling |
| C18 | 0.1µF | Mic supply |
| C19 | 1µF | Mic amp |
| C20 | 0.1µF | Mic feedback |
| C21 | 0.1µF | BOOT debounce |
| C22 | 1µF | RESET debounce |

---

## 🧪 Design Considerations

- Ground plane for EMI reduction
- ESP32 antenna keep-out respected
- Separate analog routing for microphone
- Decoupling capacitors close to ICs
- USB-C CC resistors correctly implemented
- Battery charging current set safely

---

## 🧪 Testing Strategy

- Power rail validation
- USB enumeration
- Battery charge & termination test
- Sensor I²C/SPI verification
- SD card read/write
- ADC noise testing (mic & LDR)

---

## 🚀 Applications

- Environmental monitoring
- IoT data logger
- Smart sensor node
- Academic & portfolio project
- Embedded systems experimentation

---

## 🔮 Future Enhancements

- Fuel gauge IC
- Enclosure design
- OTA firmware support
- EMI compliance testing
- Low-power optimization

---

## 👤 Author

**Yukesh S**  
Embedded Systems Enthusiast  

---

## 📜 License

This project is licensed under the MIT License.

You are free to use, modify, distribute, and commercialize this design,
provided that the original copyright notice and license text are included.

See the [LICENSE](LICENSE) file for full details.

