# Klein-zmk
ZMK Firmware for Klein keyboard https://github.com/snsten/Klein


# Bluetooth Connection for Klein

![Klein BLE manual](https://user-images.githubusercontent.com/79617315/227060016-6c585598-03bb-4c95-98b2-06dce468a7f8.jpg)

1. For first time bluetooth connection, please refer to picture above. 
2. After flashing new firmware, check if the Bluetooth profile connection is still active. If it's not, proceed with Step 3.
3. Remove Klein bluetooth connection in your pc by "Remove Device" in "Bluetooth and other devices".
4. Continue with "First Time Bluetooth Connection"..
5. :warning: Pairing BLE ZMK keyboard is a two-way connection thingy. Always make sure you have "Remove Device" in your pc after flashing. 
6. :sleeping_bed: Klein will automatically wake up when a key is touched/registered. If the board doesn't wake up immediately, try spamming BLE+01 (your Bluetooth profile).


# Key Remap in ZMK 
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

# Flashing u2f to split
1. Connect left and right splits to your pc (both connect together using type c cable)
2. Put right into bootloader mode (press the reset button), one window is popped out showing "nicenano" folder. Dont do anything yet, remember this folder as right split. 
3. Now press reset button on your left split, one window will be popped out as previous step.
4. Drag left and right u2f to respective folders.
5. Do not disconnect right split yet. 
6. Remove left split from type c cable. Proceed to `Klein BLE manual` to connect your board to pc. If successfully connected, you shall able to type without cable now. 
8. If so, remove the right split from type c cable. Both should be working good now!

:star: If you like our service or products, please tell your friends and family about us so we can grow and offer more options in the future. We strive to provide comprehensive user manuals to save you time exploring our products. We welcome any suggestions you have to help us improve our boards.




