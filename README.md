# 🚀 Pre-Practica: IoT-Based Environmental Monitoring with WiFi  

## 📖 Overview  
This project utilizes a **Waspmote IoT device** to collect **environmental sensor data** (temperature, humidity, and gas levels) and transmit it via **WiFi** to a remote server (Meshlium).  

✅ **Connects to a WiFi network** and retrieves network details.  
✅ **Reads sensor data** from a gas sensor module (temperature, humidity, pressure).  
✅ **Sends data to a Meshlium gateway** using HTTP.  
✅ **Manages power efficiently** by turning sensors on/off.  

---

## 🛠 Hardware & Technologies  
- **Microcontroller**: Waspmote IoT Board  
- **WiFi Module**: WaspWIFI_PRO_V3  
- **Sensors**:  
  - **BME Gas Sensor (bmeGasesSensor)** → Measures **temperature, humidity, pressure**  
- **Communication Protocols**: HTTP over WiFi  
- **Power Management**: Optimized to switch sensors ON/OFF when needed  

---

## 📌 How the Code Works  

### **1️⃣ Initialize WiFi & Connect to Network**
```cpp
char SSID[] = "LANCOMBEIA";
char PASSW[] = "beialancom";
error = WIFI_PRO_V3.configureStation(SSID, PASSW, WaspWIFI_v3::AUTOCONNECT_ENABLED);
```
- Connects to the **LANCOMBEIA WiFi network** with the provided credentials.  
- If connected successfully, it prints the **SSID, IP address, MAC address, and signal strength**.  

---

### **2️⃣ Set Up Environmental Sensors**  
```cpp
bme.ON();
float temperature = bme.getTemperature();
float humidity = bme.getHumidity();
float pressure = bme.getPressure();
bme.OFF();
```
- **Turns on the BME gas sensor** to measure **temperature, humidity, and pressure**.  
- **Turns off the sensor after reading** to **save power**.  

---

### **3️⃣ Transmit Data to Meshlium Server**  
```cpp
char host[] = "82.78.81.171";
uint16_t port = 80;
error = WIFI_PRO_V3.sendFrameToMeshlium(type, host, port, frame.buffer, frame.length);
```
- **Formats the sensor data into an HTTP request** and sends it to a **remote server** (`82.78.81.171`).  
- Uses **Waspmote's built-in frame structure** to encode the data before transmission.  

---

### **4️⃣ Power Management for Efficiency**
```cpp
PWR.setSensorPower(SENS_3V3, SENS_ON);
PWR.setSensorPower(SENS_5V, SENS_ON);
delay(10000);  // Wait 10 seconds
PWR.setSensorPower(SENS_3V3, SENS_OFF);
PWR.setSensorPower(SENS_5V, SENS_OFF);
```
- **Turns sensors ON only when needed**.  
- **Reduces power consumption** by switching them OFF after data collection.  

---

## 📂 Expected Output  
When running, the system should:  
✅ Print WiFi connection details (**SSID, IP address, signal strength**).  
✅ Read & display **temperature, humidity, and pressure** from the gas sensor.  
✅ Send data to **Meshlium (IP: 82.78.81.171)** via **HTTP**.  
✅ Manage power by **turning sensors ON/OFF dynamically**.  

---

## ⚙️ Customization  
### **1️⃣ Change WiFi Network**  
Modify these lines with your WiFi credentials:  
```cpp
char SSID[] = "YOUR_WIFI_NAME";
char PASSW[] = "YOUR_WIFI_PASSWORD";
```

### **2️⃣ Change Server Address**  
Update the `host` variable to **send data to a different server**:  
```cpp
char host[] = "NEW_SERVER_IP";
```

### **3️⃣ Adjust Power Management Timing**  
Modify the **delay duration** to control sensor activation frequency:  
```cpp
delay(5000);  // Reduce to collect data every 5 seconds
```

---

## 🚀 Next Steps  
🔹 **Would you like to store sensor data in a cloud database?**  
🔹 **Need to add more sensors (CO2, dust, VOCs)?**  
🔹 **Want real-time graph visualization of the collected data?**  

Let me know how to improve it! 📡🔥  
