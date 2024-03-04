# About
This repository contains a Node-RED flow designed to interface with digital light control and window shading control systems using a Raspberry Pi and Pico-W. It includes both Apple HomeKit and Nodered-UI features, allowing you to control your smart home directly from your iOS or Android device. It is a better alternative to the [homebridge-tcp-smarthome](https://github.com/RajkumarGara/homebridge-tcp-smarthome) project.

[![Smart window control video](img/7.GIF)](https://youtu.be/M36LoMouvPg)

## Working procedure
Using the Node-RED platform with the [SmartHome.json](./SmartHome.json) flow on a Raspberry Pi allows for the control of lighting and window coverings in a home automation setup. This system can handle commands for turning lights on or off, specifically designed for [`LMDI-100`](./docs/LMDI_Serial_Protocol.pdf) devices, as well as manage window coverings through [`Mechonet`](./docs/Mecho_Shade_Serial_Protocol.pdf). When an accessory is operated via Apple HomeKit or the Node-RED user interface, Node-RED sends a command to the appropriate command pipe. These pipes are established by the [PtyServer](https://github.com/RajkumarGara/remote-serial-pico/blob/main/src/PtyServer.js) software, which connects to each [Pico-W](https://github.com/RajkumarGara/remote-serial-pico/blob/main/src/PicoSerialClient.py) unit over TCP. The commands are then relayed by the Pico-W to the connected devices using RS232 communication. It captures and shows responses from the Pico-W in Node-RED for easy monitoring and troubleshooting. Installing several Pico-W units in a building, all linked to the same WiFi network as the Raspberry Pi, allows for centralized management of various devices.

## Features
1. Accessories can be operated through either Apple HomeKit or Nodered-UI.
2. It supports light and window covering accessories.
3. Number of accessories can be configured. (Refer [`Configure accessories`](#Configure-Accessories) section).
4. It sends LMDI-100, Mechonet commands to the Pico-W through command pipe and records their response to response pipe.
5. Individual and all lights on/off.
6. Individual light brightness control from 0 to 100%.
7. All window blinds 5-level (0%, 25%, 50%, 75%, 100%) covering.

## Installation
* Install [nodered on Raspberry-Pi](https://nodered.org/docs/getting-started/raspberrypi) by running this command on Pi's terminal.
    ```bash
    bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
    ```  
* Install [nodered-red-dashboard](https://flows.nodered.org/node/node-red-dashboard) and start the node-red service.
    ```bash
    cd ~/.node-red
    npm i node-red-dashboard
    node-red-restart
    sudo systemctl enable nodered.service
    node-red-start
    ```  
* Refer [NRCHKB](https://github.com/NRCHKB/node-red-contrib-homekit-bridged?tab=readme-ov-file#easy-install) to install HomeKit package on nodered.

## Running the Setup
* Follow the instructions in [import export flow](https://flowfuse.com/blog/2023/03/3-quick-node-red-tips-5/#1.-copy-and-share-your-flows-using-export-and-import) to import [`SmartHome.json`](./SmartHome.json) to the nodered.
* Follow the instructions in [remote-serial-pico](https://github.com/RajkumarGara/remote-serial-pico) to setup the Pico-W.

## Configure Accessories
* To add accessory, copy the existing accessory (for example: Dimmable Bulb) on nodered flow.
* Increment/decrement the 'n' value (represents accessory number) in function node connected to the accessory.
* Add the accessory on your Apple device.

## Visual Overview
* This block diagram describes the complete project.
    ![Block diagram](img/1.jpg)

* Below screenshot shows the main control flow (Sending commands through serial port as well as command pipe. Displaying Pico-W response in debug window).
    ![Main control flow](img/2.jpg)

* This screenshot displays the window blinds control buttons within the Node-RED flow. The following one illustrates the same buttons within the Node-RED UI.
    ![blinds control buttons](img/3.jpg)

    ![blinds control buttons UI](img/8.jpg)

* This screenshot shows the light control buttons within the Node-RED flow. The following one illustrates the same buttons within the Node-RED UI.
    ![light control buttons](img/4.jpg)

    ![light control buttons UI](img/9.jpg)

* This screenshot shows the HomeKit accessories for Pico-W1 on nodered.
    ![HomeKit accessories for Pico-W1](img/5.jpg)

* This screenshot shows the HomeKit accessories for Pico-W2 on nodered. The following one illustrates the same buttons on iPad home.
    ![HomeKit accessories for Pico-W2](img/6.jpg)

    ![HomeKit accessories on iPad](img/10.jpg)

## Credits
Special thanks to [Medical Informatics Engineering](https://www.mieweb.com/) for their support throughout the development of this project, especially to [Doug Horner](https://github.com/horner) for his invaluable guidance.