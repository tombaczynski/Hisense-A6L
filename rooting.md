<!-- markdownlint-disable -->
# Hisense A6L rooting

> [!WARNING]
> Please proceed at your own risk. There are chances that performing below instructions could lead to unrecoverable phone.
The author is not responsible for any damage caused to the phone with below instructions. You have been warned.

### Pre-requisites
- Hisense A6L with 6.08.03 software
- qfil software
- Edl drivers
- ADB (Downloaded and in system Path)
- Developer Options and USB Debugging Enabled
- Installed current official Magisk (now this is `v28.1`)(https://github.com/topjohnwu/Magisk) aplikację Magisk (było v28.1). 
> [!IMPORTANT]
> **Custom Fastboot downloaded** (Dedicated to Hisense A9)
- Phone connected via USB ;)
- TWRP HLTE730T
- Downloadables [here](https://mega.nz/folder/DrIhDJhJ#SYs0sOBSO8Z5FEUjwhalEQ), possibly need to [guess pass](guess_pass.md)

### Download partitions from phone (using Windows as OS)

To do with *Qfil* (Qualcomm Flash Image Loader tool) from package *QPST* from Qualcomm.
Steps:
- Establish connection with phone: `c:\platform-tools> adb devices`  
  - Confirm connection on phone (check saving computers fingerprint for later use).  
- Reboot phone to *edl mode*: `c:\platform-tools> adb reboot edl`
- Using *Qfil* software download partitions:
  - `boot`
  - `recovery`
  - `vbmeta`
- Steps in Qfil software:
  - *Select Build Type* `Flat Build`
  - >[!WARNING]
Use the right programmer: `prog_emmc_ufs_firehose_Sdm660_ddr_30060000.elf`
  - *Select Programmer* > *Programmer Path*: `prog_emmc_ufs_firehose_Sdm660_ddr_30060000.elf`
                                            (remember Hisense A6l have emmc storage not ufs)
  - *Tools* > *Partition manager* > Confirm that you select proper programmer.
  - On list of partition click with the right button on interesting partition and press `Manage partition data`.
  - Next: `Read data...`
  - Read data are in `C:\Users\<your_username>\AppData\Roaming\Qualcomm\QFIL\COMPORT_8` what is visible in *Status* area in main window.
  - *Qfil* saves them with `*.bin` extension. Change that to `*.img`. That is respectively: `boot.img`, `recovery.img`, `vbmeta.img`.
    (If you want backup all device with qfil you need patch.xml + programmer)
### Patching 
Move `boot.img` to the phone.
Install Magisk from trustworthy source (e.g. its [GitHub repo](https://github.com/topjohnwu/Magisk))  
- Install Magisk in you `boot.img`. Like this: [YouTube](https://www.youtube.com/watch?v=Wyl8asPGWUs)
- Download patched file to computer.

### Unlock bootloader[^1]
>[!NOTE]
>Due to lack of `fastboot` drivers on Windows in this moment I have moved to Linux (which was Mint 21.2).  
>File returned from Magisk on the phone move to that computer.  
>`adb` installed e.g. by `sudo apt install adb` command.  
In Settings > Other settings > Developer options:  
*USB debugging* `enabled`  
and
*OEM unlocking* `enabled`

### Preparation
- Establish connection with phone: `$ adb devices`  
  - Confirm connection on phone (check saving computers fingerprint for later use).  
- Reboot phone to bootloader: `adb reboot bootloader`  

### Unlocking bootloader
- With phone booted in bootloader check connection with mentioned custom fastboot:  
  `#./fastboot devices`  
- You should see device ID (serial number) (on Windows shorter: `fastboot devices`)[^2]

Following steps were doubtfull for me.
- `#./fastboot Hisense unlock`

And right after that[^3]:
- `#./fastboot erase avb_custom_key`[^4]

- Phone will reboot and display a message in Chinese to confirm a complete data wipe.Press Volume Up and wait.
Once phone restarts, you will need to setup phone again.
Confirm if bootloader is unlocked, goto Settings> Other settings > Developer Options. Under OEM unlocking. Option should be unavailable and greyed out.  

<!--Your phone "Bootloader is already unlocked"-->

### Flashing rooted `boot.img`

- Again enable *usb debugging*  
- Authenticate connection 
- Reboot to bootloader: `$ adb reboot bootloader`  
- You have to see on screen info that `DEVICE STATE` is `unlocked`
- Now flash boot patched by magisk: `# ./fastboot flash boot boot.img`
- Optionally, you can also flash custom recovery: `# ./fastboot flash recovery twrp_HisenseA6L.img`
- Vbmeta... `# ./fastboot flash vbmeta --disable-verity --disable-verification vbmeta.img`
- `# ./fastboot continue` to reboot

Be happy with root 


[^1]: Possibly helpful for someone tips from [aimindseye](https://github.com/aimindseye) form [Hisense A9 `unlockbootloader.md`](https://github.com/aimindseye/hisense-a9/blob/main/unlockbootloader.md)  
Steps to Unlock Bootloader (using Windows as OS)  
• Open two command prompt windows (if using Linux, then terminal windows).  
• In first window, goto directory where adb is installed if adb is not in system path  
• In second window, goto directory where custom fastboot is downloaded  
• In first window, enter following command  
    ◦ `adb reboot bootloader` (if using Linux, use `./adb`)  
• In second window, enter following commands  
    ◦ To verify the Fastboot connection, type in the below command and you should get back the device ID.  
    ◦ `fastboot devices`(if using Linux, use `./fastboot`)  

[^2]: If you are not getting any serial ID, then please install the Fastboot Drivers before proceeding further.

[^3]: That is that what worked for me - maybe it was problem with cable - in the end I used a different one than at the beginning.

[^4]: If you get any errors or do not get any response using fastboot commands then it means you are not using custom fastboot. Repeat the above steps using custom fastboot.


