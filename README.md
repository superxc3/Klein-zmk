# Klein-zmk
ZMK Firmware for Klein keyboard https://github.com/snsten/Klein.
This is an individual private fork belongs to XC. Please fork [Klein-zmk](https://github.com/snsten/Klein-zmk) to edit keymap.


# Bluetooth Connection for Klein

|![Klein BLE manual](https://user-images.githubusercontent.com/79617315/227060016-6c585598-03bb-4c95-98b2-06dce468a7f8.jpg)|
|:-|
|For first time bluetooth connection, please refer to picture above. Please test the board before flashing new firmware to avoid complicated troubleshoot process.|


# Key Remap in ZMK (use Keymap Editor)
|Tutorial|
|:-|
|1. Please fork [Klein-zmk](https://github.com/snsten/Klein-zmk).|
|![image](https://github.com/superxc3/Klein-zmk/assets/79617315/0332d3da-8b21-4201-ac8a-4a7d189f27e0)|
|2. Go to [Keymap Editor](https://nickcoutsos.github.io/keymap-editor/) to edit your keymap.|
|3. If you are not sure, you can refer to our [Corne Key Remap](https://github.com/superxc3/zmk-config-crkbd#key-remap) for steps by steps screenshot.|
|4. After you click LATEST, it directs you to this webpage. Click firmware and extract the two uf2 out. Drop to left and right respectively.|

## Flashing uf2 to split
1. Connect left and right splits to your pc (both connect together using type c cable)
2. Put right into bootloader mode (press the reset button), one window is popped out. Dont do anything yet, remember this folder as right split. 
3. Now press reset button on your left split, one window will be popped out as previous step.
4. Drag left and right u2f to respective folders.
5. If you dont have extra usb c cable...You can do right first, then quickly move to left so the right can sync with left.
6. If you already tested the board before flashing, your board should be able to connect to pc without cable now.
7. Check your bluetooth device list, if Klein flashes "conneccted" between "paired", you have to BTCLEAR every profile. Remember to forget device on your pc too. Then reconnect it. Check [Bluetooth connection](https://github.com/superxc3/Klein-zmk/edit/main/README.md#bluetooth-connection-for-klein).
8. If you have any problems, please refer to session below for troubleshooting process. Alternately, you can join [ZMK discord server](https://discord.com/invite/sV4ufxFUGX) to ask for questions.

## Common Issues and Troubleshooting
1. [Mac or Window OS connected but not responding](https://zmk.dev/docs/features/bluetooth#macos-connected-but-not-working), this is working for Bluetooth 5.2 Windows.
2. Do I have power toggle button for Klein: No for our builds ya. Just touch to wake the board. If it does not connected, try to: tap BT1(if this is the one you connected), tap BT2 (new profile), tap BT1 again.
3. [This](https://drive.google.com/drive/folders/1_3GUFMp0BSCjuQMZ5hEts1PbZzonGxvo?usp=drive_link) is the default firmware that we used to flash your board. Please refer to [Flashing uf2 to split](https://github.com/superxc3/Klein-zmk/edit/main/README.md#bluetooth-connection-for-klein) to flash your boards. The reset button is on the mcu, please unscrew two screws on the cover (if you have one). 
<img src="https://user-images.githubusercontent.com/79617315/227065691-f3a060b8-b526-4b9b-9ca2-a06f01eb3be2.jpg" width="700" >

# Key Remap in ZMK (traditional way)
Guide to flash with new key map through Github actions
1. Fork this repo
2. Edit keymap  
3. Commit changes
4. Go to `Actions`, click `Build`, `Run workflow`.
5. Download the firmware from the `Actions` tab.

| Editing Keymap for ZMK firmware |
|---|
|<img src="https://user-images.githubusercontent.com/79617315/227062821-cc980eaf-55ff-420a-8b8c-a25d6c1db505.png" width="700" >|
|1. Go to [snsten/Klein-zmk](https://github.com/snsten/Klein-zmk), click `Fork` to clone to your github account|
|<img src="https://user-images.githubusercontent.com/79617315/227063210-7e008d0f-ffc0-48c9-ae36-6e6d2fcb96b7.png" width="700" >|
|2. Head to `Klein-zmk` in your fork, like mine showing `superxc3`, and that should be your name. Then go to the directory as highlighted in the photo above. |
||
|3. Now you can start edit your keymap, refer to [Keyboard Codes of ZMK](https://zmk.dev/docs/codes) to insert correct codes. Also, beware of the prefix like `&kp`, `&mt` etc. |
|<img src="https://user-images.githubusercontent.com/79617315/227064231-ec3aff68-11a5-4dfb-8be1-6da7aee1c706.png" width="700" >|
|4. After you've edited the keymap, go to `Actions` wait for compilation. If everything goes smoothly, download `firmware` to get the zip file.|
|<img src="https://user-images.githubusercontent.com/79617315/227065691-f3a060b8-b526-4b9b-9ca2-a06f01eb3be2.jpg" width="700" >|
|5. Refer to `abcde` above for flashing.|

## Example of keycodes for ZMK remap
The default firmware does not support mousekeys. However, the encoders on both sides are working as written and prepared by author snstein. For additional features, please refer to the ZMK website. If you have any questions, you can ask in their Discord server. The following are some basic and essential keycodes:


### Single tap
Always remember their prefix `&kp` or `&trans` or `to` etc. Refer to [Keyboard Codes of ZMK](https://zmk.dev/docs/codes).

### Hold
The most basic `&lt 5 Z` means hold to access layer 5, tap as z; while `&mt LSHIFT TAB` means hold as modifier Left Shift, tap as Tab.


### Macro
You can copy the following and edit according to your needs. Just need to note that for Left Shift+X it is `&macro_press &kp LSHFT &macro_tap &kp X &macro_release &kp LSHFT`; while single key tap for example c8 is `&macro_tap &kp C &kp N8`. In key remap, use `&gmail` to register macro.

```
/ {
    macros {
		gmail: gmail {
        compatible = "zmk,behavior-macro";
        label = "ZM_gmail";
        #binding-cells = <0>;
        wait-ms = <10>;
        tap-ms = <10>;
        bindings = <&macro_tap &kp X &kp C &kp H &kp C &kp L &kp O &kp W &kp AT_SIGN &kp G &kp M &kp A &kp I &kp L &kp PERIOD &kp C &kp O &kp M>;
        };

    };
};
```



:star: If you like our service or products, please tell your friends and family about us so we can grow and offer more options in the future. We strive to provide comprehensive user manuals to save you time exploring our products. We welcome any suggestions you have to help us improve our boards.




