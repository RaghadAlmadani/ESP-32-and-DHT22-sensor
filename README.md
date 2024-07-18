# ESP-32-and-DHT22-sensor
Designing and programming circuit that contain ESP with sensor or any electrical component using [Wokwi](https://wokwi.com/).
### Ddefintions:
<img src="https://www.crowdsupply.com/img/76e8/wokwi-logo_png_organization-profile.png" width="200" />

- <code style="color: yallow">Wokwi</code> -> is an online platform that provides a simulation environment for developing and testing Arduino and ESP32 projects. It allows users to create virtual circuits and simulate their behavior without the need for physical hardware.
<img src="https://th.bing.com/th/id/R.5a203790c6d463fc747cf2007d948a8a?rik=9pYH81ElNRjrqg&pid=ImgRaw&r=0" width="200"/>
  
- <code style="color: gray">ESP 32</code> -> is a versatile, low-cost microcontroller with built-in Wi-Fi and Bluetooth capabilities. It suitable for a wide range of applications, from IoT devices to wearables. Additionally, it supports various programming environments, including Arduino and ESP-IDF, allowing developers to easily create connected projects.
<img src="https://www.majju.pk/assets/uploads/2018/10/DHT22-Sensor-Pinout-2048x1688.png" width="200"/>
  
- <code style="color: yallow">DHT22 sensor</code> -> is a digital temperature and humidity sensor. It provides accurate measurements of temperature (from -40 to +125°C) and humidity (from 0 to 100% relative humidity) with a relatively fast response time.
<img src="https://th.bing.com/th/id/R.5c9c5c3b265a6af05fcb653c487d2dac?rik=e4kzPAUct938mw&riu=http%3a%2f%2fwww.raspberrypi-spy.co.uk%2fwp-content%2fuploads%2f2015%2f04%2flcd_i2c_screen_01.jpg&ehk=G9RWh6XvLtW%2bdonJpiNyYxO9FVk6LNT%2frr53Mz9znXA%3d&risl=&pid=ImgRaw&r=0" width="200"/>
  
- <code style="color: green">I2C LCD screen</code> -> is a type of liquid crystal display (LCD) that uses the I2C (Inter-Integrated Circuit) protocol for communication. This allows for easier connections and reduced wiring compared to traditional LCD setups.

--------------------------------------
### Humidity and Temperature measuring:
Hardware Required:
1. ESP 32
2. DHT22 sensor
3. I2C LCD screen<br>


![Screenshot 2024-07-16 220615](https://github.com/user-attachments/assets/ccb91f60-0509-47a3-8293-9536e8f4868a)

``` C++
#include <DHT.h>                      // Libary for DHT22
#include <LiquidCrystal_I2C.h>       // Libary for LCD
#define DHT_PIN 15                  // define the connection pin
#define DHT_Type DHT22             // define the type of the DHT if its DHT22 or DHT11
DHT dht(DHT_PIN,DHT_Type);        // Creation of DHT object instance
LiquidCrystal_I2C lcd(0x27,16,2);  // I2C address 0x27, 16 column and 2 row

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
~~~
