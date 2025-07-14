# Group_2

**Project**: Real-Time IoT Monitoring System using ESP32, MQTT, Node-RED, InfluxDB, and Grafana
**Goal**: Read temperature from a DHT11 sensor with ESP32 and send the data to Grafana

---------------------------------------------------

### 1. Wire DHT11 to ESP32
![IMG_20250624_114434_627](https://github.com/user-attachments/assets/aaa55c7c-d2f1-445c-a8bf-84e01116e2b0)
![IMG_20250624_114502_954](https://github.com/user-attachments/assets/f94c8293-35d6-442b-9113-21ad07159a18)

### 2-3. Code for temperature reading and displaying in serial monitor:
  First, ensure that the ESP32 board is already wired to your device.
  The code is located in the (esp32-mqtt) folder.

### 4. Connect ESP32 with WIFI
  ![image](https://github.com/user-attachments/assets/81b409cb-4e38-40e4-8648-e1f1d4f21fcb)
  First, locate this part of the code. Then just fill in the credentials of the wifi that you are currently connected to in the required fields.
  The MQTT part will be mentioned in the next step.

### 5-6. What is *MQTT*, and how do we send data from ESP32 to MQTT?
  According to the official MQTT website, *MQTT* is an OASIS standard messaging protocol for the Internet of Things (IoT). It is designed as an extremely lightweight publish/subscribe messaging transport that is ideal for connecting remote devices with a small code footprint and minimal network bandwidth. 
  Now, to send data from ESP32 to MQTT, we will be using **Mosquitto**, which is an open-source MQTT broker.
  ***WINDOWS:*** MQTT Broker (Mosquitto) setup:
  Link: ![Hosting a Mosquitto Server on Windows: A Step-by-Step Tutorial](https://shop.theengs.io/blogs/news/installing-mosquitto-on-windows-and-make-it-accessible-from-your-local-network)
  The website includes:
  - Installing and making Mosquitto accessible from your local network
  - Configuring Windows Firewall to allow port 1883 through to run Mosquitto properly
  - Creating users/passwords
  - Editing your *mosquitto.conf* file to make it run smoothly on your local device

  Next, install MQTT Explorer from this link: ![MQTT Explorer](https://mqtt-explorer.com)
  What is MQTT Explorer? -> MQTT Explorer is a comprehensive MQTT client that provides a structured overview of your MQTT topics and makes working with devices/services on your broker dead-simple.

  After setting Mosquitto up, you should have a user & pass prepared. Fill in the necessary fields below in the code:
  ![image](https://github.com/user-attachments/assets/6f0c225f-c83d-4bfd-b29f-fb7e5b2df2e0)
  For the mqtt_server area, you fill it with your IP address as you are running it locally on your device. Run "ipconfig" in Command Prompt, then copy & paste your IPv4 Address into the field.

  Now, let's use MQTT Explorer to see the data update in real time.
  ![image](https://github.com/user-attachments/assets/b8ee38c4-a67c-4f0c-920e-990a64ae76df)
  For 'name', just name it whatever you want.
  For 'host', copy and paste your IPv4 address. Keep the port the same.
  For 'username' and 'password', fill them in again like you did earlier.
  Click connect, then you should be able to see the sensor. Click it, then you'll be able to see the data on the MQTT broker.


---------------------------------------------------

### 1. Set up Node-RED and InfluxDB
  *To set up Node-RED:
  1. Go to: https://nodered.org
  2. Click get started -> run locally -> getting started -> running locally
  3. The website then provides you with detailed information on how to download and set it up on your local device properly
  4. The command will execute, and you will have to click on the link that says "Server now running at... " 

  *To set up InfluxDB:
  1. Go to: https://www.influxdata.com/downloads/
  2. Scroll and find InfluxDB OSS 1.x
  3. Change 'Platform' settings to fit your own needs
  4. Installed InfluxDB locally
  5. Connected Node-RED → InfluxDB using influxdb-out node
  6. Converted incoming JSON into Influx Line Protocol using function node
  7. Verified sensor data is stored correctly using InfluxDB CLI
<img width="1280" height="657" alt="image" src="https://github.com/user-attachments/assets/dc1dac40-1683-44f1-93d6-851e922f7164" />

📂 Measurement: weather2
📈 Fields: temperature, pressure, altitude

### 2. Grafana
*Grafana Dashboard
Includes the following:

- Real-time line charts for:

1. Temperature (°C)

2. Pressure (hPa)

3. Altitude (m)

<img width="940" height="665" alt="image" src="https://github.com/user-attachments/assets/37e87e8d-9394-45e7-8f20-f8b91e027d06" />
<img width="913" height="670" alt="image" src="https://github.com/user-attachments/assets/ccf1cf24-7cc7-489e-a84a-6b5b3711b807" />

- Thresholds: e.g., show red if temperature > 30°C

- Annotations: automatic highlights when threshold exceeded

- Alerts: sent to Telegram when condition is met

-> Data source: *InfluxDB (configured with InfluxQL)*

*Telegram Alerting
Flow detects when temperature > 30°C and sends a custom Telegram message:

Example:
“⚠️ High Temp: 32.27 °C”
<img width="1280" height="938" alt="image" src="https://github.com/user-attachments/assets/5e92d682-59c4-4785-ab51-b50d7f3c7719" />


You must:
- Create a Telegram bot via @BotFather
- Obtain your bot token and chat ID
- Configure the HTTP node or use a Telegram output node in Node-RED

**How to Run
-Flash ESP32 with the Arduino sketch

-Start Mosquitto MQTT broker (or use public one)

-Import Node-RED flow and deploy

-Start InfluxDB and create database "iot_data"

-Run Grafana, configure InfluxDB as a data source

-Import or build panels in Grafana

Watch real-time updates, configure alerts and thresholds
...
  


