# Handheld RFID Reader

This repository contains the complete design files, firmware, software, and documentation for a **Handheld High-Frequency (HF) RFID Reader**. This project was developed as a partial fulfillment of the requirements for the module **EN 2161: Electronic Design Realization** at the Department of Electronic & Telecommunication Engineering, University of Moratuwa.

### 📋 Table of Contents

- [Features](#-features)
- [System Architecture](#️-system-architecture)
- [Hardware Design](#️-hardware-design)
- [Antenna Parameters](#-antenna-parameters)
- [PCB Design](#-pcb-design)
- [Enclosure Design](#-enclosure-design)
- [Software & Firmware](#-software--firmware)
- [Gallery](#-gallery)
- [Installation](#-installation)
- [Usage](#-usage)
- [Project Team](#-project-team)
- [Acknowledgments](#-acknowledgments)

### ✨ Features

- **Ergonomic Design**: A comfortable, gun-shaped enclosure with an ergonomic handle, designed in SolidWorks and 3D printed for industry-level durability
- **HF RFID Capability**: Reads HF (13.56 MHz) RFID tags, supporting the ISO 15693 standard
- **Wireless Connectivity**: Integrated ESP8266 Wi-Fi module for direct communication with a cloud database, offering greater range and flexibility compared to Bluetooth
- **Modular PCB Design**: Three separate 2-layer PCBs for the Antenna, MCU, and Power circuits to ensure signal integrity and simplify debugging
- **Rechargeable Power System**: Powered by two 18650 Li-Ion batteries (total capacity ~3600 mAh), with a dedicated charging cradle and a Battery Management System (BMS) for safety and longevity
- **User Interface**: 
  - LED indicators for power, Wi-Fi status, and read confirmation
  - A comprehensive Web Application (Node.js) for system management, data visualization, and device configuration
  - A cross-platform Mobile Application (Flutter) for on-the-go data access and monitoring
- **Centralized Database**: Utilizes Supabase (PostgreSQL) for robust, scalable, and secure data storage with row-level security policies

### 🛠️ Hardware Design

### Key Components

| Component | Selected Model | Reason for Selection |
|-----------|----------------|---------------------|
| **RFID Frontend** | NXP PN5180 | High performance, excellent documentation, and support for ISO 15693 |
| **Microcontroller** | Atmel ATmega32U4 | Native USB support, sufficient I/O, and strong community support |
| **Wi-Fi Module** | Espressif ESP8266 | Direct internet access, high data throughput, and large developer community |
| **Battery** | 2x Li-Ion 18650 (3600 mAh) | High capacity for full-shift operation, good availability, and safety |

### 📡 Antenna Parameters

A custom 2-turn PCB trace antenna was designed for the 13.56 MHz frequency. The design was simulated and optimized for performance.

| Parameter | Value | Unit | Description |
|-----------|--------|------|-------------|
| **Operating Frequency** | 13.56 | MHz | HF RFID frequency |
| **Target Impedance** | 20 | Ω | Antenna impedance |
| **Antenna Dimensions** | 65 x 65 | mm | Physical size |
| **Number of Turns (N)** | 2 | - | Antenna coil turns |
| **Track Width (w)** | 500 | µm | PCB trace width |
| **Gap between tracks (g)** | 500 | µm | Spacing between traces |
| **Simulated Inductance** | 891 | nH | Calculated inductance |
| **Simulated Capacitance** | 2.3 | pF | Calculated capacitance |
| **Simulated Resistance** | 1.180 | Ω | Calculated resistance |

### 🔧 PCB Design

The system uses a modular approach with three separate 2-layer PCBs: **Antenna**, **MCU**, and **Power**. This separation minimizes interference and simplifies manufacturing.

### PCB Modules

| PCB Module | Function | Features |
|------------|----------|----------|
| **Antenna PCB** | RF signal processing | Custom antenna design, impedance matching |
| **MCU PCB** | Main processing unit | ATmega32U4, PN5180 interface, ESP8266 communication |
| **Power PCB** | Power management | BMS, charging circuit, voltage regulation |

![Antenna PCB](images/Antenna_Top.png) ![MCU PCB](images/MCU_Top.png)

## 🏠 Enclosure Design

The enclosure and charging cradle were designed in **SolidWorks** for ergonomics, durability, and ease of assembly. The final models were 3D printed using ABS material.

### Design Features
- **Ergonomic gun-shaped design** for comfortable handheld operation
- **Robust ABS construction** for industrial durability
- **Integrated charging cradle** for convenient storage and charging
- **Professional finish** suitable for commercial applications

![RFID Reader Final Design](images/rfid_reader_final.png) 
![Charging Cradle](images/charging_cradle.png)

### Database Architecture

The backend uses **Supabase**, which provides a PostgreSQL database, authentication, and real-time APIs. The schema is designed to store information about users, readers, tags, and scan events.

![Database Schema](images/database_schema.png)
*Database Schema (from Software Report.pdf)*

### Applications

#### Web Application
- **Technology**: Node.js
- **Features**: System management, data visualization, device configuration
- **Interface**: Responsive dashboard for administrators

#### Mobile Application  
- **Technology**: Flutter (Cross-platform)
- **Features**: On-the-go data access, real-time monitoring
- **Platforms**: iOS and Android support

![Web Dashboard](images/web_dashboard.png) ![Mobile Dashboard](images/mobile_dashboard.png)
*Application Interfaces (from EDR_Design_Report.pdf)*

## 📸 Gallery

### Final Product
![3D Printed Final Product](images/final_product.png)
*3D Printed Final Product (from EDR_Design_Report.pdf)*

## 🚀 Installation

### Hardware Setup
1. **Assembly**: Follow the assembly guide in `/docs/assembly_guide.pdf`
2. **PCB Installation**: Install the three PCB modules in the enclosure
3. **Battery Installation**: Insert two 18650 Li-Ion batteries
4. **Charging**: Place the device in the charging cradle

### Software Installation
1. **Firmware Upload**: 
   ```bash
   # Upload ATmega32U4 firmware
   avrdude -p atmega32u4 -c avr109 -U flash:w:rfid_reader.hex
   
   # Upload ESP8266 firmware
   esptool.py --port /dev/ttyUSB0 write_flash 0x00000 esp8266_firmware.bin
   ```

2. **Database Setup**:
   - Create a Supabase account
   - Import the database schema from `/database/schema.sql`
   - Configure environment variables

3. **Web Application**:
   ```bash
   cd web-app
   npm install
   npm start
   ```

4. **Mobile Application**:
   ```bash
   cd mobile-app
   flutter pub get
   flutter run
   ```

## 📱 Usage

### Basic Operation
1. **Power On**: Press and hold the power button
2. **Wi-Fi Connection**: Device automatically connects to configured network
3. **Tag Reading**: Point the antenna toward an RFID tag and press the trigger
4. **Data Sync**: Scan data is automatically synchronized to the cloud database
5. **Monitoring**: View real-time data through web or mobile applications

### Configuration
- Access the web dashboard to configure device settings
- Manage user permissions and access levels
- Monitor device status and battery levels
- Export scan data in various formats

## 👥 Project Team

This project was a collaborative effort by the following team members:

| Index No. | Name |
|-----------|------|
| 220235V | Ilukkumbura I.M.E.I.B. |
| 220212A | Hapuarachchi H.A.D.N.D. |
| 220162T | Fernando C.S.R. |
| 220221B | Hathurusingha H.A.R. |
| 220420J | Nawarathne M.A.A.K. |
| 220700T | Wickramasinghe S.D. |
| 220089B | Cooray M.S.T. |
| 220163X | Fernando D.S. |

## 📄 Documentation

### Available Reports
- **[Design Report](docs/EDR_Design_Report.pdf)**: Complete hardware design documentation
- **[Software Report](docs/Software_Report.pdf)**: Software architecture and implementation details
- **[Assembly Guide](docs/assembly_guide.pdf)**: Step-by-step assembly instructions
- **[User Manual](docs/user_manual.pdf)**: Operating instructions and troubleshooting
