# Smart Home Controller with ESP32

## Introduction 🚀
This project revolves around creating a smart home controller using the ESP32 microcontroller, integrating LED control and servo motor manipulation through a web interface. The system utilizes WebSockets for real-time communication, providing a seamless user experience. Below, we'll break down the code and explain how it works.

## Hardware Components 🔌
- **ESP32**: A powerful microcontroller with built-in Wi-Fi and Bluetooth capabilities.
- **LEDs**: Three LEDs connected to pins 26, 2, and 33.
- **Servo Motor**: Connected to pin 13, used for angular movement control.

## Wi-Fi Setup 🌐
```cpp
const char *ssid = "UIU-CAIR";
const char *password = "12345678";
```
The system connects to the specified Wi-Fi network using the SSID and password provided. Once connected, it enables the ESP32 to communicate with a web server and clients via WebSockets.
---

## WebSocket Integration 💻
```cpp
AsyncWebServer server(80);
AsyncWebSocket ws("/remote");
```
The server listens on port 80, and WebSocket communication occurs through the endpoint /`remote`.
---

## LED Control 💡
```cpp
void toggleLED(int pin) {
  int pinState = digitalRead(pin);
  pinState = !pinState;
  digitalWrite(pin, pinState);
}
```
This function toggles the state of the LEDs between ON and OFF based on the current state. It's controlled via WebSocket messages.
---

## Servo Motor Control 🔄
```cpp
Servo servo1;
servo1.write(servoValue);
```
The servo motor’s position is controlled through WebSocket messages by adjusting its angle, which is set in degrees.
---

## WebSocket Message Handling 📡
```cpp
void handleWebSocketMessage(void *arg, uint8_t *data, size_t len) {
    // Handles incoming WebSocket messages
}
```
This function processes incoming messages, determines whether to control the LEDs or the servo motor, and sends responses back to the clients.
---

## WebSocket Event Management ⚙️
```cpp
void onEvent(AsyncWebSocket *server, AsyncWebSocketClient *client, AwsEventType type, void *arg, uint8_t *data, size_t len) {
  // Manages different WebSocket events like connection, disconnection, and data reception
}
```
This function handles various WebSocket events, such as connecting and disconnecting clients, and ensures that data is processed appropriately.
---

## Setup and Configuration 🛠
```cpp
void setup() {
  Serial.begin(115200);
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  
  ESP32PWM::allocateTimer(0);
  ESP32PWM::allocateTimer(1);
  ESP32PWM::allocateTimer(2);
  ESP32PWM::allocateTimer(3);
  
  servo1.setPeriodHertz(50);
  servo1.attach(servo1pin, 500, 2400);

  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi...");
  }

  initWebSocket();
  server.begin();

  Serial.println("Connected to WiFi");
}
```
This function initializes the serial communication, configures the GPIO pins for the LEDs, sets up the servo motor, connects to the Wi-Fi, and starts the WebSocket server.
---

## Loop Function 🔁
```cpp
void loop() {
  ws.cleanupClients();
}
```
The loop continuously cleans up WebSocket clients, ensuring smooth communication and responsiveness.
---

## Conclusion 🔒
This project exemplifies the power of the ESP32 for IoT applications, enabling remote control of hardware components via a web interface. The combination of LEDs and a servo motor provides a foundational example of how to integrate WebSockets into a smart home system. 📱🏡✨
```cpp

You can paste this into your `README.md` file on GitHub to provide a clear and organized overview of your project.
```
![Thank You](https://img.shields.io/badge/Thank%20You!-blue?style=flat-square&logo=smile)

<!-- Graphical GIF Animation -->
<div class="gif-container" style="text-align: center; margin-bottom: 20px;">
  <img src="https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExYzdob2I4cHdsdWhnbmtmYTBxbnk4cnl2YjZ1bGw5ZGZvMXBwdWc4bSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/00n6TSoGffGTLXSMPO/giphy.gif" alt="Working on it GIF" />
</div>
