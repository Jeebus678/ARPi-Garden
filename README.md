# ARPi Gardener 
## [A]rduino, [R]aspberry [Pi], Gardener. 

An automatic gardener powered with a Raspberry Pi and an Arduino nano. Combined with [Blynk](https://blynk.io/) as a user-friendly front-end, it grants incredible ease of use with plenty of room for customization. 

### Why use both an Arduino and a Raspberry Pi? 

Simply because both the Raspberry Pi and Arduino hold various advantages and disadvantages. For example, taking a picture on an ESP12 would take around 80 lines of code, yet on a Raspberry Pi it would only take 1. Reading sensor data however, follows the same logic only backwards, favoring microcontrollers over microcomputers. This approach gave the best of both worlds, and also posed as a new challenge.   

### How does it work? 

The Raspberry Pi manages all the more complex functions that interpret data, compute basic calculations, and most importantly sync with the blynk cloud. The Arduino Nano however, only knows how to receive commands and send sensor data. The intervals are static and have to be implemented before starting the blynk server, however there are options to remotely modify variables. This option makes more sense for a more broad growing approach. 

I then had the issue of figuring out how they will communicate between each other, and I went about it by creating a very basic language where letters symbolized commands. This meant sending "A" through serial would execute `digitalWrite(x, HIGH)` on the nano; "B" would do just the opposite, executing `digitalWrite(x, LOW)`. As written in `src.cpp`:

```cpp
incomingByte = Serial.read(); 
       if (incomingByte == 'A')
       {
           digitalWrite(light, LOW);
       }
       else if (incomingByte == 'B')
           digitalWrite(light, HIGH);
```

Modifying the code is very straight forward. All the blynk related code is on the Raspberry Pi under `/linux/main.cpp`, and the code for the nano is at `/src.cpp`. To add or remove a device- wire it accordingly to the nano, and interpret it to the built-in language mentioned above.
