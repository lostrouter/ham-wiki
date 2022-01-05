# Kenwood TM-D710 setup for SSTV transmit and receive

General setup
- configure external data settings on the radio
- put the radio into echolink mode
- tune to an open frequency
- setup SSTV software
- transmit and check output levels

## Configuring data mode settings on the radio

Either the A or B band of the radio can be used with SSTV software. For this guide it will use the A band. Under the AUX menu
- set 918 to `A-Band`
- set 920 to `19200 bps`

If the use of APRS is desired while working SSTV, the internal data band will need to changed
- set 930 to `B-Band`

## Put the radio into echolink mode

Putting the radio into echolink mode is required in order to use the `DATA` port on the back of the radio to send audio from the computer sound card. To enable echolink mode, cycle the `KEY` button on the main panel until `PF2` is shown. Turn off the radio. Hold down the button that was PF2 while powering on the radio. An icon should appear below `PM` on the right side of the display to signal that echolink mode is enabled. To disable echolink follow the same procedure as enabling.

## Tune to an open frequency

According to a few internet sources, 145.500, 145.600, 430.950 are SSTV calling frequencies in the US, but any open frequency space will work. 

Set the frequency on the A-Band (left side) of the radio, and make sure that it is also set for `PTT` and `CTRL`. When the computer sends a ptt signal it will begin transmitting on the side that has PTT and CTRL set.

## Setting up SSTV software

### QSSTV on a raspberry pi

TODO

### MMSSTV and YONIQ on Windows

TODO

## Check output levels

For this step a dummy load and an HT can be used. If a dummy load is not available, set the radio to low power TX and still use an HT to receive. An SDR or another ham station could be used to check levels as well.
