headslave
=========

Firmware for I2C Servo Controller  
Works with ATtiny26 and ATtiny2313

Device Description
------------------

* The servo controller is able to drive up to 10 servos on an I2C bus
* It produces PWM control signals whose pulse width is adjustable through the I2C interface
* The power supply and interface to the microcontroller is operated at 3.3V to 5.5V
* The servo motors can be operated at a higher voltage, usually 6V
* The firmware is available for 2 versions:
  * The ATtiny26
  * The ATtiny2313
* Each controller is clocked at 4MHz (internal)
* The LED blinks once when power is first applied.
* Thereafter the LED flashes briefly when the chip is accessed via I2C with the correct address

Protocol
--------

1. Send START condition
2. Send address and R/W direction bit. The device answers with ACK.
4. Send 1-10 data bytes. The device answers each byte with ACK.
5. Send STOP condition

### Address format

By default, the device address is 0b0001111.

Connecting the address pins to ground can set the corresponding address bit low:

##### ATtiny2313

Pin 13 = a0  
Pin 14 = a1  
Pin 15 = a2  
Pin 16 = a3  

##### ATtiny26

Pin 4 = a0  
Pin 7 = a1  
(a2 and a3 are always high)

Unconnected address inputs are set to high.

### Data format

* The first data byte controls servo0, the second byte controls servo 1, and so on
* Normal values are in the range 30-160 (about 95% of the average values are in this range)
* The special value 0 switches the PWM signal off.
  * Most data servos then switch to standby - they no longer take countermeasures if external forces act on it

Circuit
-------

Check out the [wiki] for more information about the [circuit](https://github.com/teslaworksumn/headslave/wiki/Circuit).

License
-------
This firmware is released under the GPL license.  
See LICENSE.

[wiki]: https://github.com/teslaworksumn/headslave/wiki "headslave wiki on GitHub"
