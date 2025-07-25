## STM32 Nucleo-H755ZI 2-Blink Debug Example

This repo is an example of how to setup dual-core debugging using the Cortex Debug VSCode Extension.

This was done on Windows 11 and also requires the ARM Toolchain and STM32CubeIDE. I can't remember the exact steps on how to set it up from the beginning. 

I referenced this issue here to set up my launch.json
https://github.com/Marus/cortex-debug/issues/1008

## How to use

Assuming you have all the dependencies, this is how you would use it:

1. To begin, place some breakpoints down.
2. Plug in STM32 board
3. Select Run and Debug or press Ctrl+Shift+D
> Important: You must start the CM7 debug ***BEFORE*** the CM4
4. At the Run and Debug drop-down menu at the top left , select **Debug CM7 - ST-Link** and click the green play button to **Start Debugging**. Wait until **Debug CM7** in the **Call Stack** menu on the left says **PAUSED ON BREAKPOINT** before continuing.
5. At that same drop-down menu, select **Attach CM4 - ST-Link** and click the green play button to **Start Debugging**. Wait until **Attach CM4** in the **Call Stack** menu on the left says **PAUSED ON ATTACH** before continuing.
6. In the **Call Stack** menu, you can see **Debug CM7** would be **PAUSED ON BREAKPOINT** and **Attach CM4** would be **PAUSED ON ATTACH**. For **Debug CM7**, click on **Continue**.
7. By now, you should see **Debug CM7** **RUNNING**. Click on **Continue** for **Attach CM4**. Both profiles should now be **PAUSED ON BREAKPOINT**.
8. On the Nucleo board, you should be able to see both Green and Yellow LEDs on. In the **Call Stack** menu, you should now be able to toggle both LEDs by clicking **Continue** for whichever specified profile you want. The CM7 controls the Green LED and the CM4 controls the Yellow LED. I have also set global variables count and count2 for each respective core for you to be able to monitor as well.
9. To end the session, you can stop both of the debugging sessions. 