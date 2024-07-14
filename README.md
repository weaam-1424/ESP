# ESP
### Design and program any electronic circuit that contains an ESP along with some sensor
* The purpose of this code is to measure temperature and humidity using the DHT22 and emit a sound sensor when the respective temperature value is exceeded.

* Below is a detailed explanation of what this code does:
1. Definition of the DHTesp library, which is used to deal with the DHT22 sensor.
2. Define GPIO pin 15 as input for DHT22 sensor data.
3. Define the type of device used (DHT22).
4. Create a dht object of type DHTesp and the discovered innovation.
5. Define GPIO pin 5 as a buzzer output.
6. In the setup() function:
   - Initiate a serial communication at a speed of 115200 baud.
   - Initialize the sensor on the specified pin.
   - Configure the buzzer pin as an output and start turning off the buzzer.
7. In the loop() function:
   - Read temperature and humidity from the sensor.
   - Print the read values ​​on the serial port.
   - Check if the temperature is higher than 30°C:
     - If so, the buzzer will turn on for one second and then off for another second.
   - Delay loop execution for 2 seconds.
* This code can be used in several different applications related to monitoring temperature and humidity and warning when certain levels are reached, such as:

1. Home environment control systems
2. Agricultural and horticultural applications
3. ndustrial applications
  * Electrical circuit design:
    <img width="242" alt="ESP 32" src="https://github.com/user-attachments/assets/5949c738-17d3-4753-acdf-4c078ceda421">

  * CODE :
```
#include <DHTesp.h>

#define DHTPIN 15     // Replace with the GPIO pin connected to DHT22 data pin
#define DHTTYPE DHTesp::DHT22

DHTesp dht;

const int buzzerPin = 5; // Replace with the GPIO pin connected to the positive (anode) of the buzzer

void setup() {
  Serial.begin(115200);
  dht.setup(DHTPIN, DHTTYPE);

  pinMode(buzzerPin, OUTPUT);
  digitalWrite(buzzerPin, LOW);
}

void loop() {
  float temperature = dht.getTemperature();
  float humidity = dht.getHumidity();

  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.print(" °C, Humidity: ");
  Serial.print(humidity);
  Serial.println(" %");

  // Check the temperature and activate the buzzer if it's above a certain threshold
  if (temperature > 30.0) {
    digitalWrite(buzzerPin, HIGH); // Turn ON the buzzer
    delay(1000);                   // Buzz for 1 second
    digitalWrite(buzzerPin, LOW);  // Turn OFF the buzzer
    delay(1000);                   // Wait for 1 second before checking again
  }

  delay(2000); // Adjust the delay as per your requirement
}
```


  
  
  
