# Arduino-Nano-ACS712-ADS1115

     Voltmeter ampmeter capacitymeter powermeter energymeter

   Workbench homemade lab power supply to monitor voltage, amperage, capacity, current power
   and power used since startup.
   I needed a currentmeter on the high side of the power line. The ones I found online
   all measured the current on the low side. So I came up with this that can be used on the
   high OR low side. The ACS712 used in this project is the 20A type.
   The accuracy of the 10 bit ADC of the Arduino is 5V / 2^10 = 4,88mV per step ( 2^10 = 1024).
   The ADS1115 on the other hand has 15 bits and one bit for "plus" or "minus" which results 
   in 6.144 ( = default gain amplifier of the ADC) / 2^15 = 0.187mV. The ADS1115 has four 
   analog inputs it is easy to connect the voltage divider and the current sensor to this 
   module. The maximum sample rate for the ADS1115 is 860 times per second so the delay 
   between readings has to be at least 2 milliseconds.

   The resolution of the 10 bits ADC of the arduino for the current is about 48.8mA per step.
   The resolution of the 15 bits ADC of the ADS1115 for the current is 1.875mA per step.

   The display will be updated every 500 milliseconds.
   All information has to be visible at one screen with the focus on voltage and current.

   Following hardware is used to perform the monitoring:
      - Arduino Nano
      - ST7735 full color 1.8 inch SPI display 128 x 160
      - ACS712 ± 20A current sensor
      - voltage divider with R1 and R2 ( R1 connected to Vin and R2 to an Arduino pin and Gnd
      - ADS1115 I2C voltage sensor

       _________________________________________
      |  1  |  2    3    4    5    6    7    8  |
      | VCC | GND  CS   RST  D/C  SDA  SCK  LED | PINOUT SPI TFT 1.8 inch
      |_____|___________________________________|

    Arduino   ST7735      ACS712     ADS1115

       5V    VCC/LED       VCC         VCC  
      GND      GND         GND         GND  
       D7      RST
       D8     A0/DC
       D9      CS
      D11    SDA/MOSI
      D13      SCK
       A4                              SDA
       A5                              SCL
                           OUT        ads.A0
                                      ads.A1      out on resistor divider
