PORTING GUIDE V2 FOR ANDROID to ANDROID

Requirements tools: (Download from release page)

- Root access (Magisk recomended or you can use root access from KernelSU or Apatch if you can gain su access in termux)
- Termux
- MT manager
- UKA modules
---
NOTE: this guide for doing porting using xiaomi.eu rom as port rom
---

BEFORE YOU START:
Download the provided config file from my github release page to use it later in the guide!

GUIDE START:
1. Extract super.img.0-13 from xiaomi.eu rom to separate folder (ROM you want to port)
2. Open termux and do
   ```
    apt update && apt install android-tools
   ```
4. Open extracted super.img folder
   ```
    cd /sdcard/"YOUR FOLDER"
   ```
6. Merge split super.img by doing
   ```
    simg2img super.img.0 super.img.2 super.img.4 super.img.5 super.img.6 super.img.7 super.img.8 super.img.9 super.img.10 super.img.11 super.img.12 super.img.13 superimgname.img
   ```
8. Open MT manager and Move merged super.img into data/local/UnpackerSuper/
9. Open termux to Extract super.img
    ```
    su
    ```
    ```
    menu
    ```
    ```
    3 (menu: Unpacking .img)
    ```
    ```
    2 (Unpacking .img from folder: data/local/UnpackerSuper/)
    ```
    ```
    Select superimgname.img
    ```
    ```
    return(enter)
    ```
11. Extract system.img
    ```
    3 (menu: Unpacking .img)
    ```
    ```
    2 (Unpacking .img from folder: data/local/UnpackerSuper/)
    ```
    ```
    Select system.img
    ```
    ```
    return(enter)
    ```
13. Do the same for mi_ext.img, product.img and system_ext.img
17. Add files from previous guide to extracted .imgs
18. Open MT Manager and open extracted .img folder
19. Make new folder like this:
    ```
        mi_ext_a
        System_a
        Product_a
        System_ext_a
    ```
    Then move extracted folders to new created folders Example: mi_ext move to mi_ext_a
12. Open config/"extracted_img"/ and move all config files to separated folders as backup
13. Copy provided config from ROM_FILES.zip and add it to UnpackerSystem/config Note: backup the original config files first
14. Open termux and build .img
    ```
    su
    ```
    ```
    menu
    ```
    ```
    7 (menu: Building .img)
    2 (menu: Build .img(raw))
    3 (Build. img(raw) with the size of the folder for assembly)
    Select build folder
    ```
    Do the same for system_ext_a, system_a, product_a and system_ext_a
    Theres a new .img created inside UnpackerSystem/ folder usually named as "partition_name"_a_new.img
    Rename it to "Partition_name"_a.img Example: mi_ext_a_new.img to mi_ext_a.img
16. Move the new .img to extracted UnpackerSuper/ folder
17. Open termux and merge .img
    ```
    su
    ```
    ```
    menu
    ```
    ```
    7 (Build .img)
    3 (Build super.img)
    2 (Build super.img(raw))
    ```
    Note: if you build with "sparse" format, you can't flash the rom using Orangefox(custom recovery) or fastboot only!
19. Import new super.img from UnpackerSuper/output/ to INSTALLER folder
20. Rename from super_new.img to super.img or any name you want. but make sure you change the name in the installer script inside "META-INF/com/google/android/updater-script"
21. Zip the folder and flash it using custom recovery or fastboot.
