### Vehicle OBD reader
A read-only Wi-Fi dashboard for the Ather 450X, running on an ESP32-C3 with a CAN transceiver. It is built on top of the open-source Ather OBD Reader by SAM0-0 and keeps all of its original screens.

What's added: a new "Extra" tab that shows more live details from the scooter, including:

- Cell temperatures, humidity and other battery-side temperatures
- Pack current and state of energy
- Charge and discharge current limits
- Per-cell state of charge
- Odometer
- Firmware versions of the scooter's modules
- Battery identification number

How it works: connect the board to the scooter, join the board's Wi-Fi network, and open the dashboard in your phone's browser. The device only listens and never sends anything to the scooter.


###  Trademark Disclaimer
this is an unofficial hobby project, not affiliated with Ather Energy. Use it at your own risk.
