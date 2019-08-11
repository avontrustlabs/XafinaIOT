# Smartwater - Water and Laundry Management

/*-----( Import needed libraries - NOTE Must in Documents/Arduino as a folder called libraries same folde as sketch folder. Set COM4 port ) (c) 2019 Avontrust. First developed for P&G Laundry Management System using Arduino Uno -----*/

#include <Wire.h>  // Comes with Arduino IDE
#include <LiquidCrystal_I2C.h>
#include <dht11.h>
 
LiquidCrystal_I2C lcd(0x3f,16,2);  // set the LCD address to 0x27 for a 16 chars and 2 line display 
 
dht11 DHT11;
 
/* Define the DIO pin that will be used to communicate with the sensor */
#define DHT11_DIO 2
 
void setup()
{
 
 lcd.init();                      // initialize the lcd 
  lcd.backlight();
   lcd.begin(16,2);   // initialize the lcd for 16 chars 2 lines, turn on backlight
  lcd.print("ADB Smartwater");
   delay(1000);


}

/* Main program loop */
void loop()
{
  /* Perform a read of the sensor and check if data was read OK */
  if (DHT11.read(DHT11_DIO) == DHTLIB_OK)
  {
    /* If so then output the current temperature and humidity to 
    the serial port */
  
    lcd.print("Moisture:");
    lcd.print((float)DHT11.humidity, 0);
    
        lcd.print(" %");
    
    delay(2000);
    lcd.clear();

lcd.print("Temp:");
    lcd.print((float)DHT11.temperature, 0);
    
        lcd.print(" C");
    
    delay(2000);
    lcd.clear();
  
  }else
  {
    /* If there was a problem reading from then sensor then output 
    an error */
    lcd.println("DATAERROR!");
  }
   
  delay(500);
}
