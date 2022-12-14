# Creality_Ender_3_S1_Pro [![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/) [![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FFUEL4EP%2FCreality_Ender_3_S1_Pro&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com) <a href='https://ko-fi.com/FUEL4EP' target='_blank'><img height='20' style='border:0px;height:20px;' src='https://cdn.ko-fi.com/cdn/kofi1.png?v=2' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

# Cura 4.13 settings for Creality Ender 3 S1 Pro 3D printer

Since my new Creality Ender 3 S1 Pro 3D printer almost drove me crazy, here my currently best setting for this new printer after a lot of frustrating testing, try and error, and debugging. With these settings and recipces I hope that you can have a better jump start and do not need to go through the same frustration cycles as I had to do. There are for sure possibilities to further improve the Cura settings. Still some small zits are visible in the test print. I am curious to get your feedback. Any feeback and further improvements are highly welcome.

## Download of these recipes

- You can dowload these recipes at Github [here](https://github.com/FUEL4EP/Creality_Ender_3_S1_Pro/releases/latest)

## Forum Discussions

- Some forum discussions about the Auto Bed Leveling of a Creality Ender 3 S1 Pro printer can be found [here](https://forum.drucktipps3d.de/forum/thread/20617-ender-3-s1-pro-abl-probleme-oder-zu-bl%C3%B6d/)

## Used filament

- PLA with diameter 1.75 mm, color: white

## Used Cura version

- Cura 4.13.0

## Operating System

- Kubuntu 18.04
- If you have a different operating system, please adapt below instructions and guidelines appropriately. I personally do only have Linux OS and do not know details of other operating systems.

## Firmware of Creality Ender 3 S1 Pro

- First check whether your printer has the fitting hardware version:
    + The required HW Mainboard Version is **V2.4.S1.301**
    + The required mainboard CPU is an **ARM STM32F401**, see [here](./STM32F401_CPU.png). Ths [video](https://youtu.be/UMbQarMeT_Q) shows how to open the bottom cover of the printer. 
    + The required hardware version is **CR-FDM-v24S1_301**
    + Please check it in the touchpad [at Settings/About](./about.png)
    + If you have a different H/W version, the below described firmware update will **NOT** work.
    + If your H/W version is **CR-FDM-v2.5.S1_1**, an updated firmware seems not to be available from Creality. Then skip this firmware upgrade step.

- Download the latest firmware from [here](https://www.creality.com/pages/download-ender-3-s1-pro)
- **UPDATE 05th Dec 2022**: There is a new firmware [Ender-3 S1_Pro_HWv24S1_301_SWV2.0.8.24F4_FDM_LASER](https://img.staticdj.com/7dd7a212124f0e7c8153fdfbe741d140.zip) available at the Creality site since 29th Nov 2022. I've not yet tested this new version. I will do this within a couple of days and report it here.
- **UPDATE 06th Dec 2022**: The firmware binaries of the release on 1st Sept 2022 and 29th November are identical: 2.0.8.24F4. I've no idea why Creality did a new release for no obvious reason.
- **UPDATE 07th Dec 2022**: The Creality firmware updates dated 01.Sep.2022 and 29.Nov.2022 are differing just in the Readme.txt's installation instructions for the display firmware. Please follow the instructions of the latest released firmware version.
- So far I used the version  [Ender-3 S1_Pro_HWv24S1_301_SWV2.0.8.24F4_FDM_LASER 29 Nov. 2022](https://img.staticdj.com/7dd7a212124f0e7c8153fdfbe741d140.zip)
- Install the firmware according this YouTube video ['Service tutorial Ender- 3 S1 Pro flash the mainboard and screen firmware'](https://www.youtube.com/watch?v=NmoRRFW4zTc&t=81s)
- Please note also the [Release Notes](./Release_Notes_of_firmware.png) in [Creality's release page](https://www.creality.com/pages/download-ender-3-s1-pro)

## IMPORTANT

- After the firmware upgrade execute a reset to factory settings with the touch screen menu of the 3D printer.
- Without a factory reset the saving to EEPROM does not work!

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
- **WARNING**: **These recipies were tested only with Cura 4.13.0. Cura 5.x ist behaving completely different and won't work with these recipies.**

## Initial settings with Pronterface 

### Establish a connection
-  First check that you can connect Pronterface to your Ender 3 S1 Pro printer. Click on 'connect' in Pronterface's GUI. You should get [this message](./Pronterface_connection_is_established.png) in the Pronterface console.
### Factory Reset
- Do a factory reset by entering ['M502' G code command into the Pronterface console](./M502_factory_reset.png). You should get [these outputs](./M502_factory_reset_outputs.png).
- Then check that the EEPROM is writable by issuing a ['M500' command](./M500_save_to_eeprom.png) in the Pronterface console input. You should get the shown outputs '..echo:Settings Stored ..'
- **IMPORTANT**: After a factory reset, the XYZ distance from the nozzle to the probe trigger-point [is set wrongly](M851_correct_distance_nozzle_touch_pin.png) to 'M851 Probe offset X-40.00 Y-40.00 Z0.00. Therefore, auto bed leveling (ABL) is not working reliably and as expected.
### Correct the probe offset
- Please set now the correct probe offset by a command ['M851 X-31.8 Y-40.50' followed by 'M500'](M851_correct_distance_nozzle_touch_pin.png) and verify the result by a 'M851' G code command.
### Determine the optimum z-offset
- The Z-offset of the 'M851'probe offset is still zero and needs now to be adjusted to your printer specifically.
- For that purpose, firstly do a [manual leveling of the bed](https://www.youtube.com/watch?v=Oa5nWPuc6is) with a piece of paper using the Ender 3 S1 Pro's touchpad GUI: First adjust the center and then the 4 corners. Repeat this 2..3 times until all corners and the center are showing the same resistance when pulling the paper.
- Now save the Z offset to EEPROM by entering 'M500' into the Pronterface's console.
- Verify the probe offset again by a 'M851' G code command. The Z Offset should now be updated and fitting to your printer hardware.
- My **recommendation** is to print the 5 squares test structure (see below) and to observe carefully the print of the first layer. **During the print**, you can adapt with the touchpad  the z-offset in small increments or decrements to get the best layer adhesion. Note and use this z-offset for yuor subsequent prints.
### Update the PID parameters of the temperature controllers
- Next, we are now updating the PID **P**roportional???**I**ntegral???**D**erivative feedback loop parameters of the control of the bed and hotend temperatures and store the determined parameters in the EEPROM. This is done by the Pronterface G code command sequence:
#### a) For the hotend
> M303 E0 S215 C5
- the correct PID parameters are outputted as
>   #define DEFAULT_Kp \<determined P-value>  
    #define DEFAULT_Ki \<determined I-value>  
    #define DEFAULT_Kd \<determined D-value>
- Now set these determined parameters by a G code sequence:
>   M301 P\<determined P-value> I\<determined I-value> D\<determined D-value>  
    M500  
    M301
- In my case the outputs were as [follows](M303_PID_autotune_of_hotend.png).
#### b) For the bed
> M303 E-1 S60 C5
- the correct PID parameters are outputted as
>   #define DEFAULT_Kp \<determined P-value>  
    #define DEFAULT_Ki \<determined I-value>  
    #define DEFAULT_Kd \<determined D-value>
- Now set these determined parameters by a G code sequence:
>   M304 P\<determined P-value> I\<determined I-value> D\<determined D-value>  
    M500  
    M304
- In my case the outputs were as [follows](M303_PID_autotune_of_bed.png).
### Run the auto bed leveling (ABL)
- At first, view [this video 'Service tutorial Ender - 3 S1 Plus leveling and printing'](https://www.youtube.com/watch?v=oDpSvNdVAjI).
- At second, please follow this video ['Service tutorial Ender - 3 S1 layer shifting debugging'](https://www.youtube.com/watch?v=Io0YQGvBko0) concerning the mechanical check and necessary adjustments.
- At third, please watch and follow this video ['Ender 3 S1 Pro Auto Bed Leveling fix!'](https://www.youtube.com/watch?v=FjLng4CiktA)
- Now, let's at first preheat the bed to 67 deg C an the hotend to 215 deg C by the G code commands:
>    M190 S67
>    M104 S215
- This takes a bit and results in [these Pronterface outputs](./M190_preheat_bed_M104_preheat_hotend.png)
- After the bed and hotend temperatures are settled, run the [auto bed levelling](G28_G29_auto_bed_leveling.png) G code command sequence:
>   G28  
    G29  
    M500
- The final 'M500' is storing the correction matrix to the EEPROM. 
- In my case the outputs were as [follows](G29_output_followed_by_M500_save_to_eeprom.png).
- After auto bed leveling, a 'M503' output looks in my case as [follows](./M503_after_G29_auto_bed_leveling.png). Please note the output of the determined Bilinear Leveling Grid.
- Repeat the auto bed leveling regularly, e.g. once every two weeks.
### Reconfirm the EEPROM settings
- Finally, please enter the command 'M503' to get a [summary](./M503_after_having_done_all_settings.png) of the updated EEPROM settings.

### Use of a digital gauge for mechanically checking the bed leveling

- You can use a digital gauge, e.g. [this one](https://www.amazon.de/AUTOUTLET-Messtaster-Messbereich-Indikator-Indicators/dp/B092278DRT), for checking the leveling of the bed.
- A suitable 3D printable holder 'S1 Dial Gauge v1.stl' can be downloaded from [here](https://media.printables.com/media/prints/177982/stls/1667253_1678fe08-46c3-4ab4-beba-6f18e169e04a/s1-dial-gauge-v1.stl)
- You need additional three suitable M3 skrews and a M3 nut.
- Here some pictures of the installed digital gauge:
    + [Picture of installed digital gauge 1](./digital_gauge_1.png)
    + [Picture of installed digital gauge 2](./digital_gauge_2.png)
    + [Picture of installed digital gauge 3](./digital_gauge_3.png)
- **IMPORTANT: Do not yet insert the digital gauge into the holder. Always start with a demounted digital gauge!**
- Move the X and Y axis by the touchpad menu 'Ready => Axis Move'
    + **WARNING:** Insert the digital gauge into the holder not until the home position has been reached.

## Load the provided 3D Manufacturing Format file into Cura
- Open the provided 3mf file [Creality_Ender_3_S1_Pro_Cura_4.13.3mf](./Creality_Ender_3_S1_Pro_Cura_4.13.3mf) into Cura
- Now you should have a clone of my Cura settings
- You should get this [Cura screen](./Cura_screen_after_project_load_of_3mf_file_en.png)
- There are 3 test structures included in the 3mf file:
    + 5 squares
    + 20 mm XYZ test box
    + stringing test
    
- You can split these test structures in 3 separate 3mf files easily.

- Check the correct printer settings in Cura
    + [Setting 1](./Cura_printer_settings_1_en.png)
    + [Setting 2](./Cura_printer_settings_2_en.png)
    + [Setting 3](./Cura_printer_settings_3_en.png)
 - Please ensure that the diameter of the filament is set as 1.75 mm
 - Cura settings in CSV format are [here](./Creality_Ender_3_S1_Pro_Cura_4.13_parameters.csv)
        

## Pictures

- [Picture of test structures](./teststructures_1.png)
- [Zoom picture of test structures](./teststructures_2.png)

## Always clean your 3d printer bed

- **It is absolute essential** for the adhesion of the first layer that the bed is cleaned from any fat or oil from your fingertips before starting any print.
- Use isopropyl alcohol to [clean your 3D printer bed](https://3dprinterworldexpo.com/how-to-clean-3d-printer-bed-full-guide/). Use a spray bottle. Use a microfiber cloth to clean the bed.


## Support structures

- Switch on support structures if your project requires them.

## Test print
- Do a test print
- If you are satistfied:


## Clone the settings for your own project
- The easiest way for cloning the settings is: 
    - Right click the build plate in Cura
    - Select 'Clear Build Plate' (Ctrl D)
    - Open your new STL file
- For each 3D Manufacturing Format file provided here, a parameter CSV file is provided. The CSV has been exported by Marketplace plugin 'Import Export CSV Profiles'. This plugin also allows to import CSV profiles.

- **Have fun with your 3D printer!**
## Recommended additional bedleveling tests

- [Bed Leveling Calibration test object](https://www.thingiverse.com/thing:13053)
- Print results of bedleveling-try_this_one_first.stl **with brim**:
    - [Picture 1](bedleveling-try_this_one_first_1.png)
    - [Picture 2](bedleveling-try_this_one_first_2.png)
    - [Picture 3](bedleveling-try_this_one_first_3.png)
    - [Picture 4](bedleveling-try_this_one_first_4.png)
    
## 20mm calibration cube with slightly different Cura settings
- [Here](./20mm_cube_Cura_4.13.3mf) a 20 mm calibration cube with slightly different Cura settings as 3D Manufacturing Format file:
    + Ironing is switched on for smoothing the Z side
    + The z seam is [set as user defined to behind left](z_seam_2.png).
    + Here the [Z seam in Cura](./z_seam_1.png)
    + Here the printed [X side's view](./20mm_cube_X.png)
    + Here the printed [Y side's view](./20mm_cube_Y.png)
    + Here the printed [XZ side's view](./20mm_cube_XZ.png)
    + Almost perfect :-)
- Cura settings in CSV format are [here](./20mm_cube_Cura_4.13_parameters.csv)
    
## Example of a case with slightly different Cura settings
- [Here](./case.3mf) a case of a [radiation sensor](https://github.com/FUEL4EP/HomeAutomation/tree/master/AsksinPP_developments/sketches/HB-UNI-Sensor1-RAD-AL53) with slightly different Cura settings as 3D Manufacturing Format file:
    + Inner Wall(s) Line Width: 0.35 mm
    + Infill Line Width: 0.35 mm
    + Optimize Wall Print Order: Set
    + Outer Before Inner Walls: Set
- The print is almost perfect with these settings:  
    -    [Case picture 1](case_1.png)
    -    [Case picture 2](case_2.png)
- Cura settings in CSV format are [here](./case_Cura_4.13_parameters.csv)
- Also here, observe the print of the first layer and adjust manually the z-offset for an optimum result if needed. Only if the first layer looks good, proceed with the print. Else restart and adjust the z-offset.

## Avoid the Z seam for rotationally symmetric models

- For a single rotationally symmetrical model [like this one](single_rotationally_symetrical_model.png) the z seam can be avoided by [these additional settings](rotationally_symmetrical_model_settings.png).
- However, the Cura spiral mode is working **only** for a **single** wall line, i.e. thicker walls won't work.

## 3DBenchy - The jolly 3D printing torture-test by CreativeTools.se
- Based on [Thingiverse #3DBenchy - The jolly 3D printing torture-test by CreativeTools.se
by CreativeTools April 09, 2015](./https://www.thingiverse.com/thing:763622).
- [Here](./3DBenchy.3mf) the 3DBenchy as 3D Manufacturing Format file.
- The print is quite good with these settings (printed without support structures):
    - [3DBenchy picture 1](./3DBenchy_1.png)
    - [3DBenchy picture 2](./3DBenchy_2.png)
    - [3DBenchy picture 3](./3DBenchy_3.png)
    - Cura settings in CSV format are [here](./3DBenchy_Cura_4.13_parameters.csv)

## Marlin G codes

- The used Marlin G codes are described [here](https://marlinfw.org/meta/gcode/)

## Your feedback is welcome and needed

- Please give feedback as an [Issue](https://github.com/FUEL4EP/Creality_Ender_3_S1_Pro/issues) or start a [discussion](https://github.com/FUEL4EP/Creality_Ender_3_S1_Pro/discussions)
- Any further improvement is highly welcome
- Let's try to further improve the Cura  settings for the Creality Ender 3 S1 Pro 3D printer
- Many thanks for your cooperation and help in advance

## Disclaimer

- I accept no liability or responsibility for the accuracy and completeness of the information and materials contained in this Readme.md or provided repository data. Under no circumstances I will be held liable for or responsible in any way for any claims, damages, losses, expenses, costs, or liabilities whatsoever (including, without limitation, any direct or indirect damages for loss of profits, business interruption or loss of information) resulting or arising directly from your use of or inability to use this Readme.md or any websites linked to, from your reliance on the information material on this provided information, even if I have been advised of the possibility of such damages in advance.

- I cannot guarantee the validity of the information found here. While I use reasonable efforts to include accurate and up to date information, I make no warranties as to the accuracy of the content and assume no liability or responsibility for an error or omission in the content.

- Any processes portrayed in linked videos should be used at your own risk. I have no responsibility or liability for any claims, damages, losses, expenses, costs, or liabilities whatsoever incurred as a result of watching or following the content in any linked videos.

- Updating the firmware of your Creality Ender 3 S1 Pro 3D printer may damage your printer and make it non-operational. **Any update of your printer's firmware is at your own risk.**





 
