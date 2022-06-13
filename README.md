# ตัวอย่างการประยุกต์ใช้งานบอร์ด ESP32 AC Power ProtoAutomation


<div id="top"></div>

<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://www.imiconsystem.com/">
    <img src="images/icon.jpg" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">ตัวอย่างการประยุกต์ใช้งานบอร์ด ESP32 AC Power ProtoAutomation</h3>

  <p align="center">
    เปลี่ยน Sensor ธรรมดาให้รองรับการเชื่อมต่อผ่าน Modbus RS485 Protocal
    <br />
 
`````````````````````
+---------------+                 +---------------+
| ModbusServer  |                 | ModbusClient  |
+---------------+                 +---------------+
        | ---------------------\          |
        |-| None ModBus Sensor |          |
        | |--------------------|          |
        | ------------------------\       |
        |-| ESP32 ModbusServerRTU |       |
        | |-----------------------|       |
        |                                 |
        | RS485 Protocal                  |
        |-------------------------------->|
        |                                 |
        |                                 |
        |                                 |
        |                                 |
        |                                 |
        |                                 |
        |                   Request by ID |
        |<--------------------------------|
        |                                 |
`````````````````````
  </p>
</div>


<!-- ABOUT THE PROJECT -->
## เกี่ยวกับ

การพัฒนาระบบงาน IOT นั้น การสื่อสารระหว่าง Sensor ไปยังระบบบริหารจัดการข้อมูลด้วย Modbus RS485 Protocal เป็นที่นิยมอย่างแพร่หลายเพราะประหยัดต้นทุนและจุดเด่นเรื่องความเสถียร ทั้งยังสามารถใช้ในระยะทางที่ไกลได้
หากเราสามารถนำ Sensor ที่ไม่รองรับ Modbus มาเปลี่ยนให้รองรับ Modbus RS485 ได้ น่าจะช่วยลดต้นทุนเมื่อเทียบกับการซื้อ Sensor ใหม่

## คุณสมบัติเริ่มต้น:
- ตั้งหมายเลข ID ของเซนเซอร์ผ่าน Software หรือ Jumper
- เก็บข้อมูล ID ไว้ใน EPROM ของ ESP32
- ใช้ 4 Pin สำหรับตั้งค่า ID ด้วย Binary code (max 15)
- ใช้ 1 Pin สำหรับปิด-เปิดโหมดตั้งค่า
### Function code ที่รองรับ
- Read Coils (0x01)
- Read Holding Registers (0x03)
- Write Coil (0x05)
- Write Holding Registers (0x06)
- Write multiple coils (0x0F)
- Write multiple Registers (0x10)




## อุปกรณ์
- ESP32-DOIT-DEV-KIT-v1
- RS485 to TTL coverter module
- USB to RS485 coverter module

## พัฒนาระบบด้วย

* [PlatformIO](https://platformio.org/)

## Arduino Library ที่สำคัญ
- EEPROM.h สำหรับเก็บค่าไอดีลง ROM
- ModbusServerRTU สำหรับทำ ModBus Server



<!-- GETTING STARTED -->
## Getting Started

### Wiring diagram

``````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````
+-------+           +-----------+       +-----------+ +-----------+ +-----------+
| ESP32 |           | DIPSWITCH |       | RS4852TTL | | USB2RS485 | | Computer  |
+-------+           +-----------+       +-----------+ +-----------+ +-----------+
    | ----------\         |                   |             |             |
    |-| GPIO 34 |         |                   |             |             |
    | |---------|         |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |-------------------->|                   |             |             |
    |                     | --------\         |             |             |
    |                     |-| 1 [1] |         |             |             |
    |                     | |-------|         |             |             |
    | ----------\         |                   |             |             |
    |-| GPIO 35 |         |                   |             |             |
    | |---------|         |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |-------------------->|                   |             |             |
    |                     | --------\         |             |             |
    |                     |-| 2 [2] |         |             |             |
    |                     | |-------|         |             |             |
    | ----------\         |                   |             |             |
    |-| GPIO 36 |         |                   |             |             |
    | |---------|         |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |-------------------->|                   |             |             |
    |                     | --------\         |             |             |
    |                     |-| 3 [4] |         |             |             |
    |                     | |-------|         |             |             |
    | ----------\         |                   |             |             |
    |-| GPIO 39 |         |                   |             |             |
    | |---------|         |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |-------------------->|                   |             |             |
    |                     | --------\         |             |             |
    |                     |-| 4 [8] |         |             |             |
    |                     | |-------|         |             |             |
    | ----------\         |                   |             |             |
    |-| GPIO 23 |         |                   |             |             |
    | |---------|         |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |-------------------->|                   |             |             |
    |                     | ------------\     |             |             |
    |                     |-| 5 [RESET] |     |             |             |
    |                     | |-----------|     |             |             |
    | --------------\     |                   |             |             |
    |-| GPIO 17 TXD |     |                   |             |             |
    | |-------------|     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |---------------------------------------->|             |             |
    |                     |                   | ------\     |             |
    |                     |                   |-| TXD |     |             |
    |                     |                   | |-----|     |             |
    | --------------\     |                   |             |             |
    |-| GPIO 16 RXD |     |                   |             |             |
    | |-------------|     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |---------------------------------------->|             |             |
    |                     |                   | ------\     |             |
    |                     |                   |-| RXD |     |             |
    |                     |                   | |-----|     |             |
    | ------\             |                   |             |             |
    |-| VIN |             |                   |             |             |
    | |-----|             |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |---------------------------------------->|             |             |
    |                     |                   | ------\     |             |
    |                     |                   |-| VCC |     |             |
    |                     |                   | |-----|     |             |
    | ------\             |                   |             |             |
    |-| GND |             |                   |             |             |
    | |-----|             |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |---------------------------------------->|             |             |
    |                     |                   | ------\     |             |
    |                     |                   |-| GND |     |             |
    |                     |                   | |-----|     |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   | -----\      |             |
    |                     |                   |-| A+ |      |             |
    |                     |                   | |----|      |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |------------>|             |
    |                     |                   |             | -----\      |
    |                     |                   |             |-| A+ |      |
    |                     |                   |             | |----|      |
    |                     |                   | -----\      |             |
    |                     |                   |-| B- |      |             |
    |                     |                   | |----|      |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |------------>|             |
    |                     |                   |             | -----\      |
    |                     |                   |             |-| B- |      |
    |                     |                   |             | |----|      |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |             |
    |                     |                   |             |------------>|
    |                     |                   |             |             | -----------------------------\
    |                     |                   |             |             |-| Used QModBus or QmodMaster |
    |                     |                   |             |             | |----------------------------|
    |                     |                   |             |             |

``````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````


## Installation

1. โหลดโปรเจคด้วย PlatformIO
2. Burn ลง ESP32


<!-- USAGE EXAMPLES -->
## Usage
 1. เปิดโหมดตั้งค่าโดยเลื่อนปุ่ม RESET (DIP Switch 5)
 2. เลื่อน DIP 1-4 เพื่อกำหนด ID โดยใช้ Binary code.
 3. กด Reset Esp32
 4. ปิดโหมดตั้งค่าโดยเลื่อนปุ่ม RESET (DIP Switch 5)
 5. กด Reset Esp32
 6. ทดสอบอ่าน


<!-- ROADMAP -->
## Roadmap
- [x] ตั้งหมายเลข ID ของเซนเซอร์ผ่าน Software หรือ Jumper
- [x] ตั้งค่า ID ด้วย Binary code (max 15)
- [x] เก็บ ID ไว้ใน EPROM
- [x] Reset mode
- [x] Read Coils (0x01)
- [x] Read Holding Registers (0x03)
- [x] Write Coil (0x05)
- [x] Write Holding Registers (0x06)
- [x] Write multiple coils (0x0F)
- [x] Write multiple Registers (0x10)
- [ ] Arduino Support
- [ ] Add Test
- [ ] ทดสอบติดตั้ง Sensor


<!-- LICENSE -->
## License

Private


<!-- CONTACT -->
## Contact

Imicon Dev Team - [dev@imiconsystem.com)



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [ESP32 Flash memory ](https://www.electronics-lab.com/project/using-esp32s-flash-memory-for-data-storage/)
* [Emodbus](https://github.com/imiconsystem/eModbus)

