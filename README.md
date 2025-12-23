# cc1101-esp32-esphome-fan-controller

I forked this from spetryjohnson but I wanted a non mqtt version that would work right from ESPHome in Home Assistant. I changed some of the README to make sense with my version of the project and I will eventually get it all setup but forgive me, I'm busy with my kids and they are my top priority.

This project was created to automate a [Home Decorators Collection Beckford 52in ceiling fan](https://www.homedepot.com/p/Home-Decorators-Collection-Beckford-52-in-Indoor-Brushed-Nickel-Ceiling-Fan-with-Adjustable-White-Integrated-LED-with-Remote-Control-Included-YG630-BN/318749131) from Home Depot. 

This fan uses a 303MHz RF signal, so my original approach of using a [hacked Sonoff RF Bridge](https://github.com/schmurtzm/RFLink32-For-Sonoff-RF-Bridge) wasn't going to work. 

I spent a bunch of time trying to figure out how to automate the 303MHz fan and came across a bunch of partially-working-but-partially-outdated forum posts, Github projects, etc.

This project combines everything I learned from those resources into a single project, specifically for the CC1101 version that is readily available in March 2025.

This project:
  - Will help you capture RF commands from your remote using ESPHome Builder and then create buttons for it use inside Home Assistant.
  


## Software dependencies
EspHome Builder in Home Assistant

## Materials

### CC1101 RF transceiver

The CC1101 is a common RF transceiver that supports multiple frequencies including 303MHz and 433MHz.

**There are multiple versions of this module** and many of the resources I found were for an older one. This project was written and tested using the 8-pin "v2.0" module found on [Amazon](https://www.amazon.com/dp/B0D2TMTV5Z) or [AliExpress](https://www.aliexpress.us/item/3256806768036185.html).

![Image of CC1101 module](/assets/CC1101.png)

### Ceiling fan w/ RF Remote

My fan uses this remote, which has the model number "TX028C-2" stamped on the back.

![Image of fan remote with power button, speed control button, light button, and light temp button](/assets/remote.png)


### ESP32

Any ESP32 should work, but I'm using one of the [WROOM 32 dev boards from Amazon](https://www.amazon.com/dp/B09GK74F7N).


![Image of ESP32 board](/assets/ESP32.png)

## Wiring

![Wiring schematic](/assets/wiring.png)

Pinout was found on [this datasheet](https://github.com/NorthernMan54/rtl_433_ESP/blob/main/docs/E07-M1101D-TH_Usermanual_EN_v1.30.pdf)


## Getting started 

### Step 1 - Figure out your frequency

If you don't know what frequency your fan uses you can try a web search search for the remote's FCC identifier, or you can use the Frequency Analyzer feature of a Flipper Zero.

![Frequency Analyzer flipper zero](/assets/flipper-zero-freq-analyzer.png)

### Step 2 - Capture your RF codes

Copy the yaml and update the frequency variable in the cc1101 part of the yaml.

Install the new script and monitor the output. Hit the buttons of the fan and collect the codes.

![Screenshot of commands being captured](/assets/command-capture.png)

### Step 3 - Update the yaml

Set the 'code' and the 'protocol' for each of the fan modes in the YAML under the buttons and install it again

### Step 4 - Use your buttons

Go to Settings -> Devices & Services -> ESPHome -> whatever_you_named_it

Your buttons should be in the 'Controls' area and test out your new controls.

