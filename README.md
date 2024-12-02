# Home Automation using Google Assistant

This project demonstrates a voice-controlled home automation system, allowing users to control home appliances such as lights, fans, and motors through Google Assistant. The system integrates Google Assistant, IFTTT, Adafruit IO, and an ESP8266 (NodeMCU) microcontroller to control home devices via voice commands.

## Project Overview

- **Voice Control**: The system listens for voice commands through Google Assistant.
- **Cloud Integration**: Google Assistant communicates with IFTTT to trigger actions in the Adafruit IO platform.
- **Microcontroller**: The ESP8266 (NodeMCU) microcontroller receives commands from Adafruit IO and controls the connected devices through relays.
- **Devices**: The project can control devices like lights, fans, motors, etc., connected to the relays.
- **Communication**: Communication between the microcontroller and Google Assistant is done via Wi-Fi using MQTT protocol.

## Requirements

### Hardware

- **ESP8266 (NodeMCU)**: A Wi-Fi enabled microcontroller to connect the system to the internet and control relays.
- **Relay Module**: For controlling home appliances (light, fan, motor, etc.)
- **Home Appliances**: Bulb, Fan, Motor (or any device you want to control).
- **Jumper Wires & Breadboard**: For wiring the system.

### Software

- **Arduino IDE**: Used for writing and uploading code to the ESP8266.
- **IFTTT**: A platform to create applets for Google Assistant and Adafruit IO integration.
- **Adafruit IO**: Cloud platform to send and receive MQTT messages.
- **Google Assistant**: For voice-based interaction.

## Setup Instructions

### 1. Setting up Adafruit IO

1. Go to [Adafruit IO](https://io.adafruit.com/) and create an account.
2. Create a new **feed** in Adafruit IO (e.g., `onoff` for controlling devices).
3. Note down your **Adafruit IO username** and **AIO key** (Project Auth Key).

### 2. Configuring IFTTT

1. Create an account on [IFTTT](https://ifttt.com/).
2. Set up an applet:
   - **Trigger**: Use Google Assistant (e.g., "Turn on the light").
   - **Action**: Send a web request to the Adafruit IO feed, updating its value (e.g., `1` for ON and `0` for OFF).
   
### 3. ESP8266 (NodeMCU) Setup

1. Install the [ESP8266 board](https://github.com/esp8266/Arduino) in Arduino IDE.
2. Install the following libraries:
   - **Adafruit MQTT Library**: For MQTT communication with Adafruit IO.
   - **Adafruit IO Arduino Library**: For connecting to Adafruit IO via MQTT.
   
3. Upload the code to the NodeMCU (ESP8266). In the code:
   - Replace `WLAN_SSID` and `WLAN_PASS` with your Wi-Fi credentials.
   - Replace `AIO_USERNAME` and `AIO_KEY` with your Adafruit IO details.
   - Update the MQTT feed name (e.g., `onoff`) to match the feed created on Adafruit IO.

### 4. Wiring the Relay to ESP8266

1. Connect the relay module to the ESP8266 using the following pins:
   - **Relay IN** to **D1** (GPIO5) on the ESP8266.
2. Connect your home appliances to the relay (e.g., a light bulb).

### 5. Running the Project

1. After uploading the code, the ESP8266 will connect to your Wi-Fi network and subscribe to the Adafruit IO feed.
2. When a voice command is issued to Google Assistant (e.g., "Turn on the light"), IFTTT will send a signal to Adafruit IO, which will trigger the corresponding action on the ESP8266.
3. The microcontroller will control the relay based on the received command (e.g., turning the light on/off).

## Code Explanation

- **ESP8266WiFi.h**: Library for connecting the ESP8266 to the Wi-Fi network.
- **Adafruit_MQTT.h** and **Adafruit_MQTT_Client.h**: Libraries to connect and interact with Adafruit IO using MQTT protocol.
- **MQTT_connect()**: Ensures that the ESP8266 is always connected to the MQTT broker on Adafruit IO.
- **Light1**: The feed that is subscribed to for controlling devices like the light, fan, etc.
- **Relay Control**: Based on the value received from Adafruit IO, the relay is switched on/off.

## Troubleshooting

- **Wi-Fi Connection**: Ensure that your Wi-Fi credentials are correct and your Wi-Fi network is stable.
- **MQTT Connection**: If the system isn't connecting to Adafruit IO, double-check your AIO username and key.
- **Relay Not Working**: Verify the wiring of the relay module to the ESP8266 and ensure that the appliance is correctly connected.

## Enhancements

- Add more devices and feeds to control multiple appliances.
- Use SSL for secure communication with Adafruit IO by modifying the code to use `WiFiClientSecure`.
- Create a mobile app or web interface to control devices manually.

## License

This project is open-source. Feel free to use and modify it for your own needs.

---

**Note**: Make sure to follow safety guidelines when working with electrical appliances and relays.
