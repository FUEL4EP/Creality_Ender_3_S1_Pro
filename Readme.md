# Cura settings for Creality Ender 3 S1 Pro 3D printer (under construction)

Since my new Creatlity Ender 3 S1 Pro 3D printer almost drove me crazy, here my currently best setting for this new printer after a lot of frustrating testing, try and error, and debugging. With these settings and recipices I hope that you can have a better jump start and do not need to go through the same frustration cycles as I had to do. There are for sure possibilities to further improve the Cura settings. I am curious to get your feedback. Any feeback and further improvements are highly welcome.

## Used Cura version

- Cura 4.13.0

## Operating System

- Kubuntu 18.04

## Firmware of Creality Ender 3 S1 Pro

- Download the latest firmware from [here](https://www.creality.com/pages/download-ender-3-s1-pro)
- I used the version  [Ender-3 S1_Pro_HWv24S1_301_SWV2.0.8.24F4_FDM_LASER 1 Sep. 2022](https://img.staticdj.com/5610ba6f2a2f941232db55c0ccac8f6b.zip)
- Install the firmware according this YouTube video ['Service tutorial Ender- 3 S1 Pro flash the mainboard and screen firmware'](https://www.youtube.com/watch?v=NmoRRFW4zTc&t=81s)
- Please note also the [Release Notes](./Release_Notes_of_firmware.png) in [Creality's release page](https://www.creality.com/pages/download-ender-3-s1-pro)

## IMPORTANT

- After the firmware upgrade execute a reset to factory settings with the touch screen menu of the 3D printer.

## Install 'pronterface' on your computer / laptop

- Install on your computer the [Pronterface software](https://www.pronterface.com/)
- The github repository is [here](https://github.com/kliment/Printrun)
- For Kubuntu you can install the Pronterface with
> sudo apt update  
> sudo apt install printrun
- For LINUX OS, please add the udev rule [66-3dprinter.rules](./66-3dprinter.rules) to /etc/udev/rules.d and ensure that you are member of the group dialout

## Install Cura 4.13.0 on your computer / laptop

- Cura 4.13.0 is the latest version that is still running on Kubuntu 18.04
- Download it from [here](https://github.com/Ultimaker/Cura/releases/tag/4.13.0) as an AppImage

## Initial settings with Pronterface 

- under construction, please wait a bit and check again

## Load the provided 3D Manufacturing Format file into cura
- Open the provided 3mf file [Creality_Ender_3_S1_Pro_Cura_4.13.3mf](./Creality_Ender_3_S1_Pro_Cura_4.13.3mf) into Cura
- Now you should have a clone of my Cura settings
- You should get this [Cura screen](./Cura_screen_after_project_load_of_3mf_file.png)
- There are 3 test structures included in the 3mf file:
    + 5 squares
    + 20 mm XYZ test box
    + stringing test
    
- You can split these test structures in 3 separate 3mf files easily.

- Check the correct printer settings in Cura
    + [Setting 1](./Cura_printer_settings_1.png)
    + [Setting 2](./Cura_printer_settings_2.png)
    + [Setting 3](./Cura_printer_settings_3.png)
        * Please ensure that the diameter of the filament is set as 1.75 mm
    

## Test print
- Do a test print
- If you are satistfied:


## Clone the settings for your own project

- Have fun !

## Marlin G codes

- the used Marlin G codes are described [here](https://marlinfw.org/meta/gcode/)

## Your feedback is welcome and needed

- Please give feedback as an Issue
- Any further improvement is welcome
- Many thanks in advance






 
