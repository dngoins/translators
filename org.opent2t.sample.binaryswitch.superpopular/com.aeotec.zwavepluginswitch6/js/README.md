# Aeotec Smart Switch 6

Translator for Z-Wave Smart Switch 6 from Aeotec.

Product web page: [http://aeotec.com/z-wave-plug-in-switch](http://aeotec.com/z-wave-plug-in-switch)

## Setup Your Hardware

This translator depends on the openzwave-shared node package. 

Follow the instructions for your platform from this site: [https://github.com/OpenZWave/node-openzwave-shared] 
  
The following hardware is required:

1. An Aeotec Smart Switch 6
2. A ZWave USB dongle, such as http://aeotec.com/z-wave-usb-stick

Follow the instructions that come with the device for pairing the device to your Z-Wave stick.

## Installing Dependencies
To install dependencies for this translator, run:

```bash
npm install
```

## Test Device
After everything is installed, run:

```bash
node node_modules/opent2t-onboarding-zwave/test.js -n "Smart Switch 6" -f "^Aeotec*"
```

The -f parameter is a regular expression to identify this device type by matching its ID field name. In this case, we are looking for Aeotec.

If there is an Aeotec device nearby, you should see output similar to:

```bash
Onboarding device  : Aeotec Smart Switch
advertisementLocalNameFilter : ^Aeotec*
found peripheral: {"homeId":25478028,"nodeId":3}

Copy the ID of the device that was discovered, and use that to run the translator test file:

```bash
node test -c COM3 -a "{\"homeId\":25478028,\"nodeId\":3}"
```

If the device is on and connected to the Z-Wave hub, you should see it turn on/off and change brightness per
the commands in the test file. You should also see output similar to:

```bash
Initialising OpenZWave 1.4.78 binary addon for Node.JS.
        OpenZWave Security API is ENABLED
        ZWave device db    : C:/src/open-zwave/config
        User settings path : C:\src\OT2T\translators\view1\org.opent2t.sample.binaryswitch.superpopular\Aeotec Smart Switch 6\js\node_modules\openzwave-shared\build\Release/../../
        Option Overrides : --ConsoleOutput false
connecting to \\.\COM3
turnOn called.
setBrightness called with value: 10
turnOff called.
disconnect called.
```

Let's step through what's going on here. The manifest.xml for this translator documents the onboarding type
for this translator is org.opent2t.onboarding.zwave. This basically just describes what sort of setup, pairing or
auth information is required to interact with the device. In the case of this onboarding type, success means you get
an ID parameter. This parameter needs to be provided to the translator for it to work.
