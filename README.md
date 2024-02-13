# About
This repository contains Node-RED flows designed to interface with digital light control systems using Raspberry Pi's communication protocols. The flows facilitate command transmission from Node-RED's user interface to a digital light controller, utilizing different communication methods in each version:

* **Version 1** ([`flows_v1_uart.json`](./flows_v1_uart.json)): Implements the sending of LMDI-100 commands from Node-RED UI through Raspberry Pi's UART interface for Digital Light Control. This version is ideal for direct, serial-based communication setups.
  ![flows_v1_uart](img/flows_v1_uart.png)
  
* **Version 2** ([`flows_v2_tcp.json`](./flows_v2_tcp.json)'): Enhances the system by enabling the transmission of LMDI-100 commands from Node-RED UI through Raspberry Pi's TCP interface for Digital Light Control. This version is suited for network-based control scenarios, offering a more flexible and scalable solution.
  ![flows_v2_tcp](img/flows_v2_tcp.png)

## Installation
* Install [nodered on Raspberry-Pi](https://nodered.org/docs/getting-started/raspberrypi) by running the below command.
    ```bash
    bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
    ```  
* Install [nodered-red-dashboard](https://flows.nodered.org/node/node-red-dashboard) by running the below commands.
    ```bash
    cd ~/.node-red
    npm i node-red-dashboard
    node-red-restart
    ```  
* Restart nodered to make changes take effect in Node-RED.
    ```bash
    node-red-restart
    ```

## Setting up Node-RED
* Follow the instructions in [Node-RED_flow_import](https://flowfuse.com/blog/2023/03/3-quick-node-red-tips-5/#2.-import-helpful-example-flows-provided-with-custom-nodes).

## Visual Overview
* This block diagram describes the complete project.
    ![Block diagram](img/1.jpg)

## Credits
Special thanks to [Medical Informatics Engineering](https://www.mieweb.com/) for their support throughout the development of this project, especially to [Doug Horner](https://github.com/horner) for his invaluable guidance.