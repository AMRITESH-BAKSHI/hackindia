# hackindia
hackindia zendrive code

---

ZenDrive Ultra Pro (ESP32 Offline Secure Drive)

ZenDrive Ultra Pro is a standalone, internet-free secure file storage and emergency alert system built using ESP32, SD card storage, and an asynchronous web server.

The device creates its own WiFi hotspot and allows users to securely upload, download, and manage files locally through a modern browser interface — no internet required.


---

Features

Authentication System

User registration with admin approval

Password hashing using SHA256

Two-step authentication using security questions

Forgot password recovery system

Admin master key login


File Management

Upload files to SD card

Download files

Delete files

Real-time file list updates using WebSocket

Storage usage monitoring

Upload progress bar


Admin Panel

View pending user requests

Approve users

Reject users

Real-time update notifications


Real-Time System

WebSocket-based online user counter

Emergency SOS broadcast system

Buzzer activation on SOS

Siren alert in browser


User Interface

Dark/Light mode toggle

Responsive design

Instant file search

Modern glass-style UI



---

System Architecture

User Device (Browser)
↓
WiFi (ESP32 Access Point Mode)
↓
HTTP + WebSocket Server
↓
SD Card Storage via SPI


---

Protocols Used

WiFi (802.11)

TCP/IP

HTTP

WebSocket

SPI (SD card communication)

SHA256 (password hashing)



---

Hardware Requirements

ESP32 development board

Micro SD card module

Micro SD card (FAT32 formatted)

Buzzer

Jumper wires

Stable power supply



---

Pin Configuration

SD Card CS → GPIO 5
Buzzer → GPIO 4

SPI Pins:

MOSI → GPIO 23

MISO → GPIO 19

SCK  → GPIO 18



---

Default WiFi Configuration

SSID: ZenDrive_Ultra_Pro
Password: 12345678

Important: Change the WiFi password before real deployment.


---

Security Model

Implemented:

Passwords stored as SHA256 hashes

Security answers hashed

Admin approval system

WPA2 WiFi encryption

System files hidden from file list


Not Implemented:

HTTPS/TLS encryption

Session tokens

Rate limiting

Brute-force protection


This system is intended for local offline networks only.


---

File Structure on SD Card

/users.txt → Stores user database
/siren.mp3 → Emergency alert sound
/other files → User uploaded files

User database format:

email | username | passwordHash | answer1Hash | answer2Hash | answer3Hash | approvalStatus

approvalStatus:

0 = Pending

1 = Approved



---

Authentication Flow

1. User enters email, username, and password.


2. Server validates credentials.


3. If approved, a random security question is generated.


4. User answers the question.


5. Access is granted if the answer is correct.




---

SOS Emergency System

Any connected user can trigger SOS.

All connected devices receive:

Popup alert

Siren sound


Physical buzzer activates on ESP32.



---

Storage Monitoring

The system dynamically calculates:

Total SD size

Used space

Usage percentage


Displayed in the user dashboard.


---

Installation Steps

1. Install required libraries:

WiFi

ESPAsyncWebServer

AsyncTCP

SD

SPI

mbedTLS (built-in for ESP32)



2. Upload the code to ESP32 using Arduino IDE.


3. Insert FAT32 formatted SD card.


4. Power on the ESP32.


5. Connect to the WiFi hotspot.


6. Open browser and go to: http://192.168.4.1




---

Use Cases

Offline classroom file sharing

Secure lab storage

Small office local drive

Emergency panic alert system

Rural offline document distribution

IoT security demonstration project



---

Limitations

Recommended for small number of users (~5)

Performance depends on SD card speed

No internet connectivity

No HTTPS encryption

No file size restrictions



---

Future Improvements

Add HTTPS support

Add session token system

Add login attempt limiter

Add per-user file isolation

Add file encryption

Add role-based access control

Improve SD performance using SDIO



---

License

For educational and experimental use.


---
