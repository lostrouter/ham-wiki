# Kenwood TM-D710 Falconsat-3 Setup
Falconsat-3 is am amateur radio satellite with an APRS digipeater and a Packet BBS with store-and-forward capabilities. Unlike many ax.25 systems that operate simplex, Falconsat-3 operates in a full duplex crossband configuration. Because of this, it is best to configure the TM-D710 to listen on one side of the radio and transmit on the other. 

The general setup steps are as follows:

- Configure TNC to listen on Band A and transmit on Band B
- Turn on the TNC and place it into KISS mode at 9600 baud.
- Tune in the correct frequencies for both sides of the radio
- Set up PacSat ground station software

## Configure TNC
Under the AUX menu, go to menu 930: INT. DATA BAND (PACKET) and set it to `RX:A-BAND TX:B-BAND`

This will cause the radio to listen for packet data on the left side of the radio, and transmit on the right side. When you exit the menu, you should now see a small RxD icon on the left side of the radio next to the frequency, and a TxD on the right side.

Note: Do not be confused by the menu settings for APRS (under the APRS menu). Menu 601 is confusingly titled "Internal TNC", and it contains a baud rate and data band setting like we set above, but it only applies to the built in APRS functionality on the radio (not the KISS mode that we need)

# Place radio in KISS mode and switch to 9600 baud
Sadly, there's no way to do this with the radio controls or in the menus themselves, and instead this must be done via commands sent through a serial connection to the radio.

This step assumes you have the right cables for the radio, and have successfully connected it to a computer. For the purposes of this documentation, I am using a Mac, and the com port that comes up when the radio is connected is `/dev/tty.usbserial-1430`

First, turn the Packet TNC on, by pressing the softkey on the radio labeled TNC. Continue pressing it until it says PACKET12 on the screen (it will first cycle through the APRS TNC). This indicates that the built-in TNC is ready and operating at 1200 baud. We now need to connect to the radio and switch it to 9600 baud, then switch to KISS mode.

Open a terminal and initiate a connection via the `screen` application
```
screen /dev/cu.usbserial-1430 9600
```
If you connect successfully, you should be able to hit enter and get a prompt back from the radio. Use the HBAUD command to set the baud rate
```
HBAUD 9600
```
You should receive a confirmation that the baud rate was changed, and the face of the radio should now say PACKET96.

Now, switch the radio to KISS mode
```
KISS ON
```
Finally, we need to restart the TNC for it to take effect:
```
RESTART
```
The face of the radio will indicate the TNC restarting, and at this point the serial connection will no longer be functional. Exit screen by pressing `CTRL-A + \` (hold down control, then press A, then backslash). This will prompt you if you want to exit. Answer yes.

At this point the radio is acting as a KISS modem, and will require software to perform everything else we need.

## Tune in the right frequencies
Falsonsat-3 has an uplink on vhf and downlink on uhf. 

Set the right side of the radio (the transmit side) to 145.840

Set the left side (the receive side) to 435.105. This is somewhere in the middle of the doppler range, and will need to be adjusted up or down several steps during a pass.

## Set up PacSat Ground Station software

Download and extract PacSat Ground Station software from https://www.g0kla.com/pacsat/

Start the app by clicking on the PacSatGround executable (you can open the jar directly but it wont load up the satellite information correctly).

You can go through the setup steps in the manual, but the most important part is to select the right com port and baud rate. In my example, the com port is `/dev/tty.usbserial-1430`. Set the baud rate to 9600. I have "Toggle TNC in/out of KISS mode" checked. Still experimenting with if I can find a way to issue the HBAUD command from within the software (which you can do if you check the "Send TNC custom bytes at startup box) instead of manually with screen, but so far that has not been successful.

## Test the setup
If all is configured properly, you should be able to issue commands from PacSat Ground, and see the radio transmit.

Click the Falsonsat-3 tab at the top, and then the DIR button. This should cause a series of short transmissions to take place on the right side of the radio (to the uplink frequency). If so, congratulations - you should now be ready to interact with Falconsat.