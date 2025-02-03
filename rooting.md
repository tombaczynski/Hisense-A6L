# Hisense A6L rooting

> [!WARNING]
> Please proceed at your own risk. There are chances that performing below instructions could lead to unrecoverable phone.
>The author is not responsible for any damage caused to the phone with below instructions. You have been warned.

### Pre-requisites
- Hisense A6L with 6.08.03 software
- qfil sotware
- Edl drivers
- ADB (Downloaded and in System Path)
- Developer Options and USB Debugging Enabled
- Installed current official Magisk (now this is `v28.1`)(https://github.com/topjohnwu/Magisk) aplikację Magisk (było v28.1). 
> [!IMPORTANT]
> **Custom Fastboot downloaded** (Dedicated to Hisense A9)
- Phone connected via USB ;)
 

### Steps to download from phone required partitions (using Windows as OS)
>[!WARNING]
>Use proper XML scheme for operating w partitions
Using *Qfil* software download partions:
- `boot`
- `recovery`
- `vbmeta`  
"Qfil" saves them with *.bin extension. Change extensions to *.img.
That is respectively: "boot.img", "recovery.img", "vbmeta.img".

### Patching 
Move `boot.img` to the phone.
Install Magisk from thrustworth source (e.g. its [GitHub repo](https://github.com/topjohnwu/Magisk))  
- Install Magisk in you `boot.img`. Like this: [YouTube](https://www.youtube.com/watch?v=Wyl8asPGWUs)
- Download patched file to computer.

### Unlock bootloader
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
  - Confirm connection on phone (check saving computers fingersprint for later use).  
- Reboot phone to bootloader: `adb reboot bootloader`  

### Unlocking bootloader
- With phone booted in bootloader check connection with mentioned custom fastboot:  
  `#./fastboot devices`  
- You should see device ID (on Windows shorter: `fastboot devices`)

Following steps where doubtfull for me.
- `#./fastboot Hisense unlock`

And right after that (that is that what worked for me - maybe it was problem with cabled - finally I usen another than on begining):
- `#./fastboot erase avb_custom_key`

- Phone will reboot and display a message in Chinese to confirm a complete data wipe.Press Volume Up and wait.
Once phone restarts, you will need to setup phone again.
Confirm if bootloader is unlocked, goto Settings> Other settings > Developer Options. Under OEM unlocking. Option should be unavalable and greyed out.  

<!--Your phone "Bootloader is already unlocked"-->

### Flashing rooted `boot.img`

- Again enable *usb debugging*  
- Authenticate connection 
- Reboot to bootloader: `$ adb reboot bootloader`  
- You have to see on screen info that bootloader in unlocked
- Now flash boot patched by magisk: `# ./fastboot flash boot boot.img`
- Vbmeta... `# ./fastboot flash vbmeta --disable-verity --disable-verification vbmeta.img`
- `# ./fastboot continue` to reboot

Be happy with root 

.

.

.

.

# What we need more from below?

.

 
Strony do porównania 

https://www.reddit.com/r/eink/comments/16tpr96/guide_how_to_root_the_hisense_a9/?rdt=34106 

 
https://github.com/aimindseye/hisense-a9/blob/main/rootphone.md

https://github.com/aimindseye/hisense-a9/tree/main



### Unlock Bootloader

> [!WARNING]
> Please proceed at your own risk. There are chances that performing below instructions could lead to unrecoverable phone.
The author is not responsible for any damage caused to the phone with below instructions. 

### Pre-requisites
- ADB Downloaded and in System Path
- Developer Options and USB Debugging Enabled
> [!IMPORTANT]
> **Custom Fastboot downloaded**
- Phone connected via USB ;)


### Steps to Unlock Bootloader (using Windows as OS)

- Open two command prompt windows (if using Linux, then terminal windows)
- In first window, goto directory where adb is installed if adb is not in system path
- In second window, goto directory where custom fastboot is downloaded
- In first window, enter following command
  - <code>adb reboot bootloader</code> (if using Linux, use ./adb)
- In second window, enter following commands
   - To verify the Fastboot connection, type in the below command and you should get back the device ID.
  - <code>fastboot devices</code>(if using Linux, use ./fastboot)
    
> [!NOTE]
> If you are not getting any serial ID, then please install the Fastboot Drivers. Before proceeding further
-
  - <code>fastboot Hisense unlock</code> (if using Linux, use ./fastboot)
  - <code>fastboot erase avb_custom_key</code> (if using Linux, use ./fastboot)
  - <code>fastboot continue</code> (if using Linux, use ./fastboot)
 - Phone will reboot and display a message in Chinese to confirm a complete data wipe.Press Volume Up and wait.
 - Once phone restarts, you will need to setup phone again.
 - To confirm if bootloader is unlocked, goto Settings> System & Updates > Developer Options. Under OEM unlocking, there will be "Bootloader is already unlocked"


**If you get any errors or do not get any response using fastboot commands then it means you are not using custom fastboot. Repeat the above steps using custom fastboot**
