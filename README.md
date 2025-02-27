# CIS-310-Final-Project-Gesture-Temp-Controlled-Lights
Final Project for CIS 310: Computer Org and Assembly Language. Completed by Ciaran Grabowski, Hailey Gumbs, and Yahya Daoud


## Overview:

This project utilizes an Arduino Nano with the HS300x temperature and humidity sensor, as well as the APDS9960 gesture sensor, to control RGB colors using motion gestures. Additionally, the temperature sensor enables the RGB light to adjust to warmer or cooler colors based on the detected temperature while in Temperature Mode. 

## Peripheral (peripheral.ino):

### Modes of Operation: <br/>
The system operates in two modes: Display Mode and Temperature
- Upward motion enters Temperature Mode
- Downward Motion enters Display Mode
  

### Display Mode (RGB Cycling):<br/>
1. Colors are cycled based on an additive color model, allowing transitions between Red, Yellow, Green, Cyan, Blue, and Magenta.
2. Implemented an array to store the color order: `colorArray = {Red, Yellow, Green, Cyan, Blue, Magenta}`
3. A rightward gesture increments the `currColor` variable, displaying the next color in the array.
4. A leftward gesture decrements `currColor`, displaying the previous color in reverse order.


### Temperature Mode: <br/>
1. When activated by an upward gesture, the system reads the temperature and sets the RGB color accordingly:
   - Below 0°C → Blue
   - 0°C to 10°C → Cyan
   - 25°C to 35°C → Yellow
   - Above 35°C → Red
2. If a downward gesture is detected, the system prints a message and switches back to Display Mode.
3. The function pauses for 1 second (`delay(1000)`) before checking for further input. <br/>



## Central (temp_lights_BLE):
### Overview: <br/>
The Python script runs the central processing unit for the system, utilizing three threads:
1. `serial_loop`: Reads integer values from the Arduino serial monitor that correspond to LED color values.
2. `ble_loop`: Reads temperature data from the HS300x temperature sensor via Bluetooth.
3. `app.mainloop`: Runs the GUI application to display temperature and LED color data.

### Data Queues:<br/>
Two queues facilitate communication between the Arduino and the GUI
- `data_queue`: Captures single integer values representing LED color output from the serial monitor and updates the color of the GUI label widget.
- `temperature_queue`: Stores temperature values received via Bluetooth, updating the GUI’s slider widget and displaying the temperature in a textbox widget.

### Features:
- Gesture-Controlled RGB Lighting
- Temperature-Based Color Adaptation
- Real-Time Data Visualization with a Python GUI
- Bluetooth Integration for Wireless Monitoring <br/>

## Setup and Installation:
1. Clone the repository
2. Install required libraries in Arduino IDE:
    -  APDS9960 Gesture Sensor Library
    - HS300x Temperature Sensor Library
3. Install Python dependencies:
    - `pip install pyserial customtkinter`
4. Upload peripherial.ino to the Arduino IDE and run the temp_lights_BLE python script 

## Usage:
1. Power on the Arduino and connect it to the computer.
2. Run the Python script to launch the GUI.
3. Use hand gestures to change LED colors in Display Mode.
4. Use an upward motion to activate Temperature Mode, where the LED color changes based on room temperature.
5. Use a downward motion to switch back to Display Mode.
