# Variable Baud Serial Generator

A standalone, self-sustaining utility built for the M5Stack Core. This tool generates and transmits test serial packets at adjustable transmission speeds, making it an ideal bench tool for testing UART hardware, serial parsing logic, and receiving microcontrollers.

---

## 🚀 Features

* **Dynamic Baud Switching:** Brute-forces the ESP32 UART0 peripheral to re-initialize on the fly, allowing you to cycle through standard industrial baud rates (4800, 9600, 19200, 38400, 57600, and 115200 bps) without resetting the device.
* **Continuous Packet Generation:** Automatically broadcasts a sequentially numbered test payload every second (`NaviLink_Test_Packet_[#] @ [baud] bps\r\n`) to help identify dropped packets or parsing errors on the receiving end.
* **Audio & Visual Telemetry:** Emits a tactile beep when changing speeds, alongside a soft audio chirp and a flashing on-screen indicator perfectly synced to every outgoing data packet.
* **Non-Blocking Architecture:** Built entirely with `millis()` timers rather than `delay()`, ensuring the physical buttons remain instantly responsive even while the hardware serial buffer is flushing.
* **Integrated Pin Instructions:** The physical wiring requirements are permanently displayed on the screen so you never have to look up the documentation when pulling the tool out of a drawer.

---

## 🕹️ Controls & Interface

The application utilizes the physical buttons on the M5Stack Core enclosure:

* **Button A (Left):** Step down to the next lowest baud rate.
* **Button C (Right):** Step up to the next highest baud rate.

The screen actively displays the target hardware pin, the currently selected baud rate, and a blinking pulse indicator that flashes red when a packet leaves the TX pin. 

The serial data is coming out as 8N1 (8 data bits, No parity, 1 stop bit). The ESP32 core defaults to the SERIAL_8N1 standard. This is the universal default for almost all microcontroller UART communications.

---

## 🔌 Hardware Wiring

To inject serial data from the M5Stack Core into your target device, connect two jumper wires:

1. **GND** on the M5Stack Core ➡️ **GND** on your target device.
2. **T0** (UART0 TX) on the M5Stack Core ➡️ **RX** on your target device.

*Note: Pin T0 is used specifically to isolate the serial output and prevent internal bus conflicts that exist on some legacy M5Stack bottom modules.*

---

## 💻 Software Dependencies

To compile this code in the Arduino IDE, ensure you have the **esp32** board definitions (by Espressif Systems) installed, along with the following library via the Library Manager:

* **M5Unified** by M5Stack (Handles the display, power management, audio mixing, and button debouncing).

---

## License & Credits

*   **Author:** Jody Herperger, VE5SAR  
*   **AI Assistant:** Google Gemini (Code generation & logic structuring)  
*   **License:** MIT License  

*This project is open-source. You are free to use, modify, and distribute this software in your own projects. Please retain the author attribution in derivative works.*

<img width="403" height="302" alt="IMG_1189" src="https://github.com/user-attachments/assets/7b48eba4-ad5b-4259-8439-db17e119ca00" />
<img width="403" height="302" alt="IMG_1188" src="https://github.com/user-attachments/assets/4f9b4e83-4f38-4cd1-9948-93554e62f848" />
