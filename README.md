# Open Source AIS Transponder (Class B)

I started this project around 2015 with the intention of experimenting and eventually building something for my own boat.
I was not impressed with commercial AIS class B transponders. They seemed bloated, expensive and some of them
were particularly power-hungry. So I set out to create a lean and mean design.

In 2018 I installed this system on my boat. It is still working fine after 2 years.

[Image][images/UnitExterior.jpg?raw=True "Exterior View"]


## Overall description

### Hardware

The main difference between this design and nearly every commercial transponder is that it's a standalone unit. It contains all of its
radios and antennas and thus only needs a power + data cable to connect to the cabin. The PCBA is 1" wide so it fits inside
1" PVC pipe, which I used as the antenna base. The GNSS receiver and antenna are on the board. 

On the hardware side, the design is based on two Silicon Labs 4463 transceiver ICs and an STM32L432KBU6 microcontroller.
The GNSS is a Telit SE873 (7x7mm module) and relies on a Johanson ceramic SMD antenna. It usually takes about a minute to acquire a fix outdoors.
The transmitter output is 2 Watts (+33dBm) and it has a verified range of over 10 nautical miles with a vanilla telescopic antenna (< 3dBi).

The unit runs on 12V and exposes a 3.3V UART for connecting to the rest of the boat's system. The UART continuously sends GPS and AIS NMEA0183 data
while listening for CLI commands. Persistent station data (MMSI, call sign, name, dimensions, etc) is stored on a 1Kbit EEPROM and is provisioned via
the CLI. If this data is not present, the device will simply run as a receiver and never transmit. 

The circuit draws about 45mA from 12V in RX mode, and spikes up to 600 mA during transmission (for about 30 milliseconds). The latest design uses an RJ45 connector
because Ethernet cable is widely available, cheap and offers enough signals to instrument controls such as "TX on/off". I have included a reference design
for a control box that I built but every boat is different, so your mileage will absolutely vary.


### Software

The firmware is an Eclipse CDT project that you should be able to import and build. It has a BSP architecture and build configurations for different
board revisions. It contains snippets of STM32Cube generated code, but is not structured around it.

### Building the unit

This is going to be difficult for all but the most technically advanced, so I am going to be selling it as a kit (most likely on tindie.com). The kit will include a mostly-finished PCBA as well as the VHF antenna, enclosure and sealing components. The ethernet cable and whatever lies on the other side of it will be your responsibility, as every boat is different.

### License

CAD and firmware are licensed under GPLV3. 




