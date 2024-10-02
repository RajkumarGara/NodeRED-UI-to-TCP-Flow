## About
This repository is your go-to source for integrating digital light control and window shading systems into your smart home, using a Raspberry Pi and Pico-W. It is compatible with both iOS and Android devices through Apple HomeKit and Node-RED UI. It is a better alternative to the [homebridge-tcp-smarthome](https://github.com/RajkumarGara/homebridge-tcp-smarthome) project. 

**Ready to give your smart home an upgrade? Let's dive in!**

[![Smart window control video](img/7.GIF)](https://youtu.be/M36LoMouvPg)

## Working procedure
The [SmartHome.json](./SmartHome.json) flow in Node-RED on a Raspberry Pi enables the control of lights (connected through [`LMDI-100`](./docs/LMDI_Serial_Protocol.pdf)) and window blinds (connected via [`Mechonet`](./docs/Mecho_Shade_Serial_Protocol.pdf)) in a home automation setup. When an accessory is operated via Apple HomeKit or the Node-RED-UI website, Node-RED sends the command to the appropriate pseudo terminal (pty). These ptys are established by the [PtyServer](https://github.com/RajkumarGara/remote-serial-pico/blob/main/src/pi/PtyServer.js) software, which connects to each [Pico-W](https://github.com/RajkumarGara/remote-serial-pico/blob/main/src/pico/main.py) unit over TCP. Subsequently, the Pico-W relays these commands to the connected devices (LMDI or Mechonet) through RS232 communication. Node-RED displays the Pico-W responses in the Node-RED-UI for effective monitoring. Installing several Pico-W units in a building, all linked to the same WiFi network as the Raspberry Pi, enables centralized management of various devices.

## Features
1. Accessories can be operated through either Apple HomeKit or Nodered-UI website.
2. It supports lights and window covering accessories.
3. Number of accessories can be configured.
4. Individual and all lights on/off control.
5. Individual lights brightness control from 0 to 100%.
6. Individual and all window blinds 5-level (0%, 25%, 50%, 75%, 100%) covering.
7. Provides the status of blinds and lights.

## Installation
* Install [nodered](https://nodered.org/docs/getting-started/raspberrypi) on Raspberry-Pi by running this command on Pi's terminal.
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

## Visual Overview
* Checkout the network diagram: [SRC](https://docs.google.com/drawings/d/1oIbP6EGNI4thhi0qzVgtGZw0lyD-F9gRc0-1tAc7O_Q/edit)
    ![network diagram](https://docs.google.com/drawings/d/1oIbP6EGNI4thhi0qzVgtGZw0lyD-F9gRc0-1tAc7O_Q/export/png)

* Writing commands to pty and reading responses from pty for each pico:
    ![Main control flow](img/2.jpg)

* Window blinds control flow: and its corresponding UI:
    ![blinds control buttons](img/3.jpg)

    ![blinds control buttons UI](img/8.jpg)

* light control buttons: and its corresponding UI:
    ![light control buttons](img/4.jpg)

    ![light control buttons UI](img/9.jpg)

* HomeKit accessories for Pico1:
    ![Pico1 HomeKit accessories](img/5.jpg)

* HomeKit accessories for Pico2: and its UI on iPad home:
    ![Pico2 HomeKit accessories](img/6.jpg)

    ![iPad home](img/10.jpg)

## Credits
Special thanks to [Medical Informatics Engineering](https://www.mieweb.com/) for their support throughout the development of this project, especially to [Doug Horner](https://github.com/horner) for his invaluable guidance.