# ESP-32-and-DHT22-sensor
Designing and programming circuit that contain ESP with sensor or any electrical component using [Wokwi](https://wokwi.com/).
### Definitions:
<img src="https://www.crowdsupply.com/img/76e8/wokwi-logo_png_organization-profile.png" width="200" />

- <code style="color: yallow">Wokwi</code> -> is an online platform that provides a simulation environment for developing and testing Arduino and ESP32 projects. It allows users to create virtual circuits and simulate their behavior without the need for physical hardware.
<img src="https://th.bing.com/th/id/R.5a203790c6d463fc747cf2007d948a8a?rik=9pYH81ElNRjrqg&pid=ImgRaw&r=0" width="200"/>
  
- <code style="color: gray">ESP 32</code> -> is a versatile, low-cost microcontroller with built-in Wi-Fi and Bluetooth capabilities. It suitable for a wide range of applications, from IoT devices to wearables. Additionally, it supports various programming environments, including Arduino and ESP-IDF, allowing developers to easily create connected projects.
<img src="https://www.majju.pk/assets/uploads/2018/10/DHT22-Sensor-Pinout-2048x1688.png" width="200"/>
  
- <code style="color: yallow">DHT22 sensor</code> -> is a digital temperature and humidity sensor. It provides accurate measurements of temperature (from -40 to +125°C) and humidity (from 0 to 100% relative humidity) with a relatively fast response time.

<img src="https://th.bing.com/th/id/R.5c9c5c3b265a6af05fcb653c487d2dac?rik=e4kzPAUct938mw&riu=http%3a%2f%2fwww.raspberrypi-spy.co.uk%2fwp-content%2fuploads%2f2015%2f04%2flcd_i2c_screen_01.jpg&ehk=G9RWh6XvLtW%2bdonJpiNyYxO9FVk6LNT%2frr53Mz9znXA%3d&risl=&pid=ImgRaw&r=0" width="200"/> <img src="https://usercontent.one/wp/www.okuelectronics.com/wp-content/uploads/2020/02/i2c00001q.jpg" width="200" /> <img src="https://th.bing.com/th?id=OIF.66k5%2bnCL1SlwJd3EzrXtUQ&rs=1&pid=ImgDetMain" width="200"/>
  
- <code style="color: green">I2C LCD screen</code> -> is a type of liquid crystal display (LCD) that uses the I2C (Inter-Integrated Circuit) protocol for communication. This allows for easier connections and reduced wiring compared to traditional LCD setups.

--------------------------------------
## Humidity and Temperature measuring:
Hardware Required:
1. ESP 32
2. DHT22 sensor
3. I2C LCD screen<br>

### Connection:

![Screenshot 2024-07-18 122302](https://github.com/user-attachments/assets/ae011b20-21f9-4089-a6d1-9558c6b9bb68)
I connected the I2C LCD which has 4 pins I connected the voltage pin with 5V on ESP32 and the ground pin with the ground pin on ESP32 additionally, I connected SDA and SCL pins with D21 and D22 respectively. Then I connected ESP32 with DHT22 that has 4 pins the pin in the left is a positive voltage pin I connected it with 3.3V on the ESP 32, the pin next to it is (SDA) the digital pin(input/output) and I conected it with D4 pin on the ESP 32, the pin in the middle right is NC pin which means it has no connection and I kept without connection, finally the right pin is a ground pin I connect with the GND on the ESP 32.  

### Coding:
First I needed to download DHT sensor library and LiquidCrystal I2C libraries from Libarary manager. Then start coding.
``` C++
#include <DHT.h>                      // Libary for DHT22
#include <LiquidCrystal_I2C.h>       // Libary for LCD
#define DHT_PIN 15                  // define the connection pin
#define DHT_Type DHT22             // define the type of the DHT if it is DHT22 or DHT11
DHT dht(DHT_PIN,DHT_Type);        // Creation of DHT object instance
LiquidCrystal_I2C lcd(0x27,16,2);  // I2C address 0x27, 16 columns and 2 rows

void setup(){
  lcd.init();                    // initialize the lcd
  lcd.backlight();              // open the backlight
  
  dht.begin();                // start DHT

}

void loop(){
  lcd.clear();                      // clear display
  float t = dht.readTemperature(); // read the temperature and assian it to the varible t as a float number
  float h = dht.readHumidity();   // read the humidity and assian it to the varible h as a float number
  lcd.setCursor(1,0);          // move cursor to  (1, 0)
  lcd.print("Measuring...");  // print message at (1, 0)
  delay(4000);               // display the above for four seconds
  lcd.clear();
  lcd.setCursor(1,0);
  lcd.print("Temerature");
  lcd.setCursor(1,1);
  lcd.print(String(t) + " deg C"); // print the value of t and we assain it to 
  delay(4000);
  lcd.clear();
  lcd.setCursor(1,0);
  lcd.print("Humidity");
  lcd.setCursor(1,1);
  lcd.print(String(h) + "%");
  delay(4000);
  
}
```
### The Result:
![Screenshot 2024-07-16 220615](https://github.com/user-attachments/assets/115c087f-413e-46a4-a5e7-406341794280)
![Screenshot 2024-07-18 122804](https://github.com/user-attachments/assets/169d2706-16af-44f9-9ebe-76b95dd91677)
![Screenshot 2024-07-18 122823](https://github.com/user-attachments/assets/d2e4438f-a1e8-4059-9d96-fcc017c3f12b)
![Screenshot 2024-07-18 122852](https://github.com/user-attachments/assets/be216440-adcf-44ba-bc91-fed11c9a3157)
I can change the hummidity and the temerature by clicking on the DHT22 while it is running. Here is the link to the [project on Wokwi](https://wokwi.com/projects/403498370373752833)

### The Challenges:
There aren't enough resources that teach Wokwi interface and Wokwi does not have block coding also I have to download the libraries manually.
