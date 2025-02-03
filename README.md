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
   <br/> <br/>
3. Open termux and do
   <br/> <br/>
    ```
    apt update && apt install android-tools -y
    ```
    ```
    termux-setup-storage
    ```
5. Open extracted super.img folder
   <br/> <br/>
    ```
    cd /sdcard/"YOUR FOLDER"
    ```
6. Merge split super.img
   <br/> <br/>
    ```
    simg2img super.img.0 super.img.1 super.img.2 super.img.3 super.img.4 super.img.5 super.img.6 super.img.7 super.img.8 super.img.9 super.img.10 super.img.11 super.img.12 super.img.13 superimgname.img
    ```
8. Open MT manager and Move merged super.img into data/local/UnpackerSuper/
   <br/> <br/>
9. Open termux to Extract .imgs
   <br/> <br/>
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
11. Extract mi_ext.img
    <br/> <br/>
    ```
    3 (menu: Unpacking .img)
    ```
    ```
    2 (Unpacking .img from folder: data/local/UnpackerSuper/)
    ```
    ```
    Select mi_ext.img
    ```
    ```
    return(enter)
    ```
12. Do the same for system.img, product.img and system_ext.img
   <br/> <br/>
13. Add files from OEM_PORT_FILES.zip inside PORT_FILES/ to extracted .imgs folder
   <br/> <br/>
14. Open UnpackerSystem .img folder
   <br/> <br/>
15. Create new folder like this:
    <br/> <br/>
    ```
        mi_ext_a
        System_a
        Product_a
        System_ext_a
    ```
    Then move extracted folders to new created folders Example: move mi_ext to mi_ext_a
    <br/> <br/>
16. Open UnpackerSystem/config
    <br/> <br/>
17. Copy provided config from ROM_FILES.zip and add it to UnpackerSystem/config Note: backup the original config files first
    <br/> <br/>
18. Open termux and build .img
    <br/> <br/>
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
    Build all mi_ext_a, system_ext_a, system_a, and product_a
    Theres a new .img created inside UnpackerSystem/ folder usually named as "partition_name"_a_new.img
    Rename it to "Partition_name"_a.img Example: mi_ext_a_new.img to mi_ext_a.img
    <br/> <br/>
20. Move the new .img to extracted UnpackerSuper/ folder
    <br/> <br/>
21. Open termux and build super.img
    <br/> <br/>
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
    ---
    Note: if you build with "sparse" format, you can't flash the rom using Orangefox(custom recovery) or fastboot only!
    ---
    <br/> <br/>
22. Import new super.img from UnpackerSuper/output/ to INSTALLER folder
    <br/> <br/>
23. Rename from super_new.img to super.img or any name you want. but make sure you change the name in the installer script inside "META-INF/com/google/android/updater-script"
    <br/> <br/>
24. Zip the folder and flash it using custom recovery or fastboot.
