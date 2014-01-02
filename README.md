Arduino Rfid Access Control With Eeprom Storage
==================================

The sketch is designed and tested to work with an ArduinoUNO and the RFID reader
from Adafruit : 'PN532 NFC/RFID controller breakout board' connected via SPI.

The sketch is an RFID (access) control system that stores RFIDs to EEPROM.
All RFID cards stored in EEPROM will be granted access, all others will be denied access.	
It is designed to work with Mifare Classic and Mifare Ultralight cards (no other cards have been tested).
To store or delete RFIDs from EEPROM a 'MASTER' card is used. The UID of the master card 
is for the time beeing hard-coded in the sketch. It has to be a Mifare Classic 4 byte card. 
When the MASTER card is read by the reader the application will remain in MASTER MODE for 30 sec.
It will include or exclude the next RFID card that is read. If the RFID is already stored in the EEPROM 
it will be erased (excluded), if the RFID is not in the EEPROM it will be stored (included) into the EEPROM.

  
INSTALLATION:
=============
This is a sketch developed to work with the Adafruit PN532 NFC/RFID breakout board,
the wiring is explained at: http://learn.adafruit.com/adafruit-pn532-rfid-nfc/breakout-wiring

	1.  Download the Adafruit-PN532 SPI library from: https://github.com/adafruit/Adafruit-PN532 and
	    put it into your Arduino IDE library folder (restart the IDE).
	2.  Load the sketch into you Arduino IDE.

>   IMPORTANT BEFORE RUNNING THE SKETCH:
-   Set the EEPROMSize constant to your Arduino's EEPROM size, do not exceed the maximum eeprom size address. You can       however shrink the eeprom size used for the UID storage by decreasing the EEPROMSize value and/or setting the           memBase to use for UID storage to a higher value than 0 (first address of eeprom).
-   You need the baud rate to be 115200 because we need to print out the data and read from the card at the same time.

	3.  Upload the Sketch and connect to the serial console.
	4.  Read a Mifare Classic 4 byte card that you want to use as your MASTER card and replace the UID (int value) from the serial console output to the sketch: uid_master = 1344082563;
	5.  Go to the setup() section and uncomment initializeEeprom(); 
	6.  Upload the Sketch again and run the sketch one time (connect to serial) and check that the eeprom address values are all 0
	7.  Comment again the initializeEeprom(); and upload it to your Arduino. Now you can use the MASTER card to store new
        RFIDs to the eeprom.

Read different RFIDs and watsh the LEDs and/or the serial console output.
The green LED indicates that an RFID is authorised (stored in eeprom).
The red LED indicates that an RFID is not authorised (not in eeprom).
The blue LED indicates that the sketch is in MASTER mode (store or delete the following RFID read from eeprom).
If all LEDs are on the eeprom is full.

To actually open a door or do other things you have to add your own code and hardware (relais for electric door etc).
Add your code in the section commented with: // open door




TODO: 
=====
create a serial CLI interface to
  - add the MASTER card interactively without needing to enter it into the sketch code manually
  - add a command to erase (format) the EEPROM for initial setup
  - enable/disable debugging output from CLI

put the EEPROM functions into a library

Acknowledgements
=======  
webnology gmbh invests time and resources to provide open source software,
please refer to our website to support us. http://www.webnology.ch/en/arduino-rfid-access-control-eeprom.html


This is a sketch developed to work with the Adafruit PN532 NFC/RFID breakout board,
you can buy it at the Adafruit store: https://www.adafruit.com/products/364

  
License
=======
This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License
for more details.
