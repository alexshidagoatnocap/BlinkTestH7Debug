## STM32 Nucleo-H755ZI 2-Blink Debug Example

This repo is an example of how to setup dual-core debugging using the [Cortex Debug](https://github.com/Marus/cortex-debug) VSCode Extension. These instructions were particularly made for the STM32 Nucleo-H755ZI development boards and use the ST-Link to debug.

This setup currently works on Windows 11 with STM32CubeIDE installed, and on Arch Linux without STM32CubeIDE.

The steps below are continually being refined to better suit more workflows and toolchains.

## Setup:

There are two ways you can set this up:
- #### With STM32CubeIDE
    - No extra setup required, but you might need to [configure the Cortex Debug settings](https://github.com/Marus/cortex-debug/wiki#vscode-settings-for-cortex-debug) to point to the right bin locations. 
- #### Without STM32CubeIDE
    - Requires: 
        - [Visual Studio Code](https://code.visualstudio.com/Download)
        - [STM32Cube for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=stmicroelectronics.stm32-vscode-extension) **(Install the prerelease version)**
            - With the VSCode extension, the ARM GNU Toolchain, STM32 Programmer CLI, and ST-Link GDB Server are provided, so you do not need to download the next two dependencies. They should be located in a stm32cube/bundles folder.
                - On Linux, they should be stored in ```/home/$username$/.local/share/stm32cube/bundles/```, but this may vary based on distro.
        - [ARM GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)
            - Cortex Debug requires arm-none-eabi gdb, nm, and objdump
            - You can either use MinGW64 installer only if you are on Windows(You must have MinGW64) or download and extract/tar the zip/archive for all platforms.
        - ST-Link GDB Server and STM32 Programmer CLI
            - You may choose to download [STM32CubeCLT](https://www.st.com/en/development-tools/stm32cubeclt.html) ***OR*** [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
            >It is also possible to also use the [open-source stlink toolchain](https://github.com/stlink-org/stlink) using st-util for the GDB Server, but its usage differs from the STM32 GDB Server from the packages above. Instructions to integrate it will come out in the future.
    - After downloading the required toolchains, [set up](https://github.com/Marus/cortex-debug/blob/master/debug_attributes.md) your [Cortex Debug extension settings](https://github.com/Marus/cortex-debug/wiki#vscode-settings-for-cortex-debug) to point to the right /bin locations. 

I referenced this issue here to set up my launch.json
https://github.com/Marus/cortex-debug/issues/1008

## How to Use:

These steps were done on Windows 11 with STM32CubeIDE. When you have all the dependencies and Cortex Debug settings configured, this is how you would use it:

1. To begin, place some breakpoints down.

    ![alt text](README_assets/image.png)

    I have added global variables count and count2 for the CM7 and CM4 cores respectively to monitor in the **WATCH** tab.

2. Plug in STM32 Nucleo-H755ZI board
3. Select Run and Debug or press Ctrl+Shift+D

    ![alt text](README_assets/image-1.png)

> Important: You must start the CM7 debug ***BEFORE*** the CM4
4. At the Run and Debug drop-down menu at the top left , select **Debug CM7 - ST-Link** and click the green play button to **Start Debugging**. Wait until **Debug CM7** in the **Call Stack** menu on the left says **PAUSED ON BREAKPOINT** before continuing.

    ![alt text](README_assets/image-2.png)

5. At that same drop-down menu, select **Attach CM4 - ST-Link** and click the green play button to **Start Debugging**. Wait until **Attach CM4** in the **Call Stack** menu on the left says **PAUSED ON ATTACH** before continuing.

    ![alt text](README_assets/image-3.png)

6. In the **CALL STACK** menu, you can see **Debug CM7** would be **PAUSED ON BREAKPOINT** and **Attach CM4** would be **PAUSED ON ATTACH**. 

    ![alt text](README_assets/image-4.png)

    For **Debug CM7**, click on **Continue**.

    ![alt text](README_assets/image-5.png)

7. By now, you should see **Debug CM7** say **RUNNING**. 

    ![alt text](README_assets/image-6.png)
    
    Click on **Continue** for **Attach CM4**. 

    ![alt text](README_assets/image-7.png)
    
    Both profiles should now be **PAUSED ON BREAKPOINT**.

    ![alt text](README_assets/image-8.png)



8. On the Nucleo board, you should be able to see both Green and Yellow LEDs on. 
    
    ![alt text](README_assets/image-10.png)

    In the **CALL STACK** menu, you should now be able to see both LEDs toggle by clicking **Continue** for whichever specified profile you want. The Green LED is on the CM7 and the Yellow LED is on the CM4. You can remove either breakpoints to let the CM4/CM7 blink programs continue running without stopping.

    You can use this menu to switch between watching the CM7 and CM4 variables 

    ![alt text](README_assets/image-12.png)

    ![alt text](README_assets/image-11.png)


9. To end the session, you can stop both of the debugging sessions. I recommend to **Disconnect** the CM4 before you **Stop** the CM7.

    >Note: You cannot stop the CM7 and debug the CM4 by itself, the CM4 requires the CM7 in order to function. 

    You can also **Disconnect** the CM4 and debug the CM7 by itself

    ![alt text](README_assets/image-14.png)
    
    ![alt text](README_assets/image-13.png)

    


