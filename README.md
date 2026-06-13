# 🐱 Automatic Cat Feeder

An automatic cat feeder project powered by the **ESP32** microcontroller and integrated with the **Arduino IoT Cloud** platform. This system allows pet owners to schedule feeding times, control the device remotely, monitor food levels, and receive real-time notifications via a smartphone application to ensure pets stay healthy and fed on time.

---

## 🌟 Key Features
* **Scheduled Feeding:** Utilizes a Real-Time Clock (RTC) system to automatically dispense precise amounts of food at pre-set times.
* **Cloud-Based Remote Control:** Connected via Wi-Fi, enabling users to trigger manual feedings and adjust schedule settings remotely through the smartphone app (Arduino IoT Cloud).
* **Smart Alert System:**
  * Uses an HC-SR04 ultrasonic sensor to continuously measure the remaining food levels.
  * Sends automated chat notifications via the cloud platform when the food level drops below 10%.
  * Triggers a buzzer sound and updates statuses on the app dashboard to keep the owner informed.
* **OLED Status Display:** Real-time on-device display showing the current time, next scheduled feeding time, and network connection status.
* **Manual Push Button:** Features a physical button on the machine for instant manual feeding, providing a fail-safe option if the Wi-Fi or cloud connection goes offline.

---

## 🛠 Hardware Architecture
* **Microcontroller:** ESP32
* **Display:** OLED Display (SSD1306 I2C)
* **Actuator:** Servo Motor (used for opening and closing the food dispenser slot)
* **Sensors:** 2x Ultrasonic Distance Sensors (HC-SR04)
* **Indicators & Alerts:**
  * 3x LED Indicators (Red, Green, Blue) for system status states
  * Active Buzzer for audible alerts and calling pets
* **Input:** Push Button for manual overriding

### GPIO Pin Mapping
| Component | ESP32 Pin | Description |
| :--- | :--- | :--- |
| **OLED Display** | SCL $\rightarrow$ 22, SDA $\rightarrow$ 21 | I2C Communication |
| **Servo Motor** | Signal $\rightarrow$ 14 | Controls dispenser opening angle |
| **Ultrasonic 1** | TRIG $\rightarrow$ 25, ECHO $\rightarrow$ 33 | Measures remaining food in the hopper |
| **Ultrasonic 2** | TRIG $\rightarrow$ 27, ECHO $\rightarrow$ 26 | Measures food level in the bowl/tray |
| **Buzzer** | Positive $\rightarrow$ 12 | Sounds alerts / Calls pet to eat |
| **Push Button**| One side $\rightarrow$ 13 | Manual feeding trigger (Hardware Interrupt) |
| **Red LED** | GPIO 4 | System status indicator (via resistor) |
| **Green LED** | GPIO 2 | System status indicator (via resistor) |
| **Blue LED** | GPIO 15 | Active dispensing indicator (via resistor) |

---

## 📂 Software & Libraries
The firmware for this project is written in **MicroPython** and utilizes the following key libraries:
* `machine` (Pin, SoftI2C, PWM, RTC) — For direct hardware and low-level peripheral control.
* `ssd1306` — For managing and rendering text on the OLED screen.
* `arduino_iot_cloud` — Connects the ESP32 to the Arduino Cloud ecosystem.
* `hcsr04` — Driver module to handle pulse configurations for ultrasonic tracking.
* `servo` — Servo motor positioning driver.
* `ntptime` — Used to fetch network time protocol standard stamps over the internet to update the RTC.

---

## 🔧 Problems & Solutions

1. **Structural Instability:** The initial build used plaswood sheet pieces joined by adhesives that were not strong enough, causing parts to detach under the heavy weight of actual cat food, leading to tilting and bending.
   * **Solution:** Upgraded to high-strength **hot glue** for a more durable bond between plaswood joints, added a supporting base structure, and securely bolted the food container onto the mainframe.
2. **Loose Wiring Connections:** During breadboard testing, jumper wires frequently slipped loose, leading to unstable system performance.
   * **Solution:** Replaced loose jumper wire connections with **permanent soldering**, drastically improving hardware structural strength, durability, and signal efficiency.

---
# 🐱 เครื่องให้อาหารแมวอัตโนมัติ (Automatic Cat Feeder)

โครงงานเครื่องให้อาหารแมวอัตโนมัติที่ขับเคลื่อนด้วยไมโครคอนโทรลเลอร์ **ESP32** ร่วมกับแพลตฟอร์ม **Arduino IoT Cloud** ช่วยให้อาหารสัตว์เลี้ยงตามเวลาที่กำหนด สามารถควบคุม คอยเฝ้าดู และรับแจ้งเตือนสถานะแบบเรียลไทม์ผ่านแอปพลิเคชันบนสมาร์ตโฟน เพื่อให้สัตว์เลี้ยงมีสุขภาพที่ดีและได้รับอาหารอย่างตรงเวลา

---

## 🌟 คุณสมบัติเด่น (Features)
* **การตั้งเวลาให้อาหารล่วงหน้า:** ควบคุมเวลาด้วยระบบ RTC (Real-Time Clock) เพื่อจ่ายอาหารตามปริมาณและเวลาที่กำหนดโดยอัตโนมัติ
* **ควบคุมผ่านอินเทอร์เน็ต:** เชื่อมต่อ Wi-Fi สั่งการและเปลี่ยนการตั้งค่าได้จากระยะไกลผ่านแอปพลิเคชันสมาร์ตโฟน (Arduino IoT Cloud)
* **ระบบแจ้งเตือนอัจฉริยะ:** * ใช้เซ็นเซอร์ HC-SR04 วัดระดับปริมาณอาหารคงเหลือ
  * ส่งข้อความแจ้งเตือนผ่านช่องแชทบนระบบคลาวด์เมื่ออาหารใกล้หมดถัง (น้อยกว่า 10%)
  * ส่งเสียงบัซเซอร์และแสดงผลสถานะเพื่อให้เจ้าของทราบ
* **แสดงผลหน้าจอ OLED:** แสดงเวลาปัจจุบัน เวลาที่จะให้อาหารในรอบถัดไป และสถานะการเชื่อมต่อเครือข่าย
* **ปุ่มกดให้อาหารแบบ Manual:** รองรับการกดปุ่มให้อาหารด้วยมือได้ทันทีที่ตัวเครื่อง ในกรณีที่สัญญาณอินเทอร์เน็ตหลุดหรือไม่สามารถเชื่อมต่อคลาวด์ได้

---

## 🛠 อุปกรณ์ฮาร์ดแวร์ที่ใช้ (Hardware Architecture)
* **Microcontroller:** ESP32
* **Display:** OLED Display (SSD1306 I2C)
* **Actuator:** Servo Motor (สำหรับเปิด-ปิดช่องปล่อยอาหาร)
* **Sensors:** เซ็นเซอร์วัดระยะทาง Ultrasonic Sensor (HC-SR04) จำนวน 2 ชุด
* **Indicators & Alerts:**
  * LED 3 สี (Red, Green, Blue) แสดงสถานะระบบ
  * Active Buzzer ส่งสัญญาณเสียง
* **Input:** Push Button (สำหรับกดให้อาหารด้วยมือ)

### การต่อขาใช้งาน (GPIO Pin Mapping)
| อุปกรณ์ | ขาของ ESP32 | รายละเอียด |
| :--- | :--- | :--- |
| **OLED Display** | SCL $\rightarrow$ 22, SDA $\rightarrow$ 21 | สื่อสารแบบ I2C |
| **Servo Motor** | Signal $\rightarrow$ 14 | ควบคุมมุมเปิดฝาถ้วยอาหาร |
| **Ultrasonic 1** | TRIG $\rightarrow$ 25, ECHO $\rightarrow$ 33 | วัดระดับอาหารคงเหลือในถัง |
| **Ultrasonic 2** | TRIG $\rightarrow$ 27, ECHO $\rightarrow$ 26 | วัดระดับอาหารในชาม/ถาด |
| **Buzzer** | Positive $\rightarrow$ 12 | ส่งเสียงแจ้งเตือน/เรียกแมว |
| **Push Button**| One side $\rightarrow$ 13 | กดให้อาหารแบบแมนนวล (Interrupt) |
| **Red LED** | GPIO 4 | ไฟแสดงสถานะระบบ (ผ่านตัวต้านทาน) |
| **Green LED** | GPIO 2 | ไฟแสดงสถานะระบบ (ผ่านตัวต้านทาน) |
| **Blue LED** | GPIO 15 | ไฟแสดงสถานะตอนจ่ายอาหาร (ผ่านตัวต้านทาน) |

---

## 📂 โครงสร้างซอฟต์แวร์ (Software & Libraries)
โค้ดในโปรเจกต์นี้เขียนด้วย **MicroPython** และมีการนำเข้าไลบรารีที่จำเป็นดังนี้:
* `machine` (Pin, SoftI2C, PWM, RTC) สำหรับควบคุมฮาร์ดแวร์
* `ssd1306` สำหรับควบคุมหน้าจอแสดงผล
* `arduino_iot_cloud` สำหรับเชื่อมต่อแพลตฟอร์ม Arduino Cloud
* `hcsr04` ไลบรารีจัดการเซ็นเซอร์ Ultrasonic
* `servo` ไลบรารีควบคุมเซอร์โวมอเตอร์
* `ntptime` สำหรับดึงเวลามาตรฐานจากอินเทอร์เน็ตมาตั้งค่าให้ RTC

---

## 🔧 ปัญหาและการแก้ไข (Problems & Solutions)

1. **โครงสร้างไม่แข็งแรง:** เนื่องจากเดิมใช้ไม้พลาสวูดและกาวบางชนิดยึดติดไม่แน่นพอ ทำให้ชิ้นงานหลุดออกจากกัน และเมื่อใส่อาหารแมวจริงซึ่งมีน้ำหนักมากทำให้ชิ้นงานเอนเอียง
   * **วิธีแก้ไข:** เปลี่ยนมาใช้ **กาวร้อน** ที่มีความเหนียวแน่นทนทานกว่าเดิม, เพิ่มฐานรองรับน้ำหนัก และทำการขันน็อตยึดถ้วยอาหารเข้ากับตัวชิ้นงานหลัก
2. **สายไฟหลุดบ่อย:** ในช่วงทดสอบสายจัมเปอร์มักจะหลุดออกจากบอร์ดทดลอง ทำให้ระบบทำงานไม่ราบรื่น
   * **วิธีแก้ไข:** เปลี่ยนจากการเสียบสายจัมเปอร์เป็นการ **บัดกรีสายไฟ** เพื่อเพิ่มความแข็งแรง ทนทาน และมีประสิทธิภาพในการนำสัญญาณสูงขึ้น

---

## 👥 สมาชิกผู้พัฒนา (Team Members)
* สโรชินี บุญฤทธิ์ 
* อภิสิทธิ์ ศักดิ์สุริยา
* ปัญปภัส วงค์แก้ว 
* ชลธิชา พุ่มพวง 
* ศศิกานต์ โคตรปัดทุม 
