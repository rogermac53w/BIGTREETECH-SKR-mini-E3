1. Install the compilation environment, We recommend vscode + platformio. If you have already installed it, please skip this step.  If not, please see [here](https://github.com/bigtreetech/Document/blob/master/How%20to%20install%20VScode+Platformio.md).
2. Download the latest Marlin 2.0 firmware from the [official GitHub website of marlin](https://github.com/MarlinFirmware/Marlin/tree/bugfix-2.0.x)
3. Compile Marlin
* In the lower left corner of the VSCode, you can see that there’s one more icon, please see the picture below, 
which is the PlatformIO plugin, and then click "Open Project" to open the project.![image](https://user-images.githubusercontent.com/25599056/60634053-0aee5d80-9e40-11e9-9658-7cac8b6d1002.png)
* After opening the project, go to the platformio.ini file and change the default environment from megaatmega2560 to BIGTREE_SKR_MINI, `env_default = BIGTREE_SKR_MINI`![image](https://user-images.githubusercontent.com/25599056/60634202-bac3cb00-9e40-11e9-9d66-089c2b925138.png)
* Then go to the Configuration.h file and modify it:

`#define SERIAL_PORT 2`

`#define SERIAL_PORT_2 -1`

`#define BAUDRATE 115200`

`#define MOTHERBOARD BOARD_BIGTREE_SKR_MINI_E3`
![image](https://user-images.githubusercontent.com/25599056/60634464-8ac8f780-9e41-11e9-9644-f2462160818a.png)
* modify X/Y/Z/E0 step motor driver type to `TMC2209`
![image](https://user-images.githubusercontent.com/25599056/60634508-b0560100-9e41-11e9-9a3a-2fc217564a15.png)
* this board support `CR10_STOCKDISPLAY` 
![image](https://user-images.githubusercontent.com/25599056/60634579-ff9c3180-9e41-11e9-91aa-ae90dbbbdd3f.png)
* go to the Configuration_adv.h file and modify the TMC2209 slave address

`#define  X_SLAVE_ADDRESS 0`

`#define  Y_SLAVE_ADDRESS 1`
  
`#define  Z_SLAVE_ADDRESS 2`

`#define E0_SLAVE_ADDRESS 3`
![image](https://user-images.githubusercontent.com/25599056/60634675-5ace2400-9e42-11e9-8441-9de7e1480962.png)
* After the modification is complete, press Ctrl+Alt+B, and platformio will automatically download the compiled component and compile it. After the compilation is successful, a firmware.bin file will be generated in the .pioenvs\BIGTREE_SKR_MINI directory. We will copy this file to the TF card of the motherboard, and then reset the motherboard, so that the firmware is burned into the motherboard, the red led D10 will always blink in the burning, After the burning is completed, D10 stop blink, and the file name in the TF card will change from 'firmware.bin' to 'FIRMWARE.CUR'