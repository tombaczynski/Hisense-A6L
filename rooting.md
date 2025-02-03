# Hisense A6L rooting

> [!WARNING]
> Please proceed at your own risk. There are chances that performing below instructions could lead to unrecoverable phone.
The author is not responsible for any damage caused to the phone with below instructions. You have been warned.

## Pre-requisites
- Hisense A6L with 6.08.03 software
- qfil sotware
- *edl drivers?*
- ADB Downloaded and in System Path
- Developer Options and USB Debugging Enabled
- Installed current official Magisk (now this is `v28.1`)(https://github.com/topjohnwu/Magisk) aplikację Magisk (było v28.1). 
> [!IMPORTANT]
> **Custom Fastboot downloaded**
- Phone connected via USB ;)
 

## Steps to download from phone required partitions (using Windows as OS)
>[!WARNING]
>Use proper XML scheme for operating w partitions
Using *Qfil* software download partions:
- boot
- recovery
- vbmeta
"Qfil" saves them with *.bin extension. Change extensions to *.img.
That is respectively: "boot.img", "recovery.img", "vbmeta.img".

## Pathing 
Move `boot.img` to the phone.

Zainstalowałem na telefonie z oficjalnego źródła 

W Magisk spatchowałem plik “boot.img” 

W tym momencie przesiadam się na komputer z Linuksem (z powodu braku sterowników do “fastboot” na Windowsie) 

(współczesny Linux Mint?) 

Spatchowany plik “boot.img” pobrałem na komputer. 

Na komputrze zainstalowałm “adb” za pomocą komendy “sudo apt install adb” 

W telefonie włączyłem “opcje programisty” i włączyłem debugowanie USB. 

Z komputera skomunikowałem się z telefonem za pomocą komendy: “adb devices”. 

W tym momencie na telefonie trzeba było uwierzytelnić połączenie akceptując klucz komputera. Dołączyłem opcję, że na stałe. 

Rebootujemy do bootloadera: “adb reboot bootloader”. 

Używam teraz programu “fastboot” przygotowanej specjalnie dla telefonu Hisense A9. 

Mając uruchomiony telefon w trybie bootloadera możemy sprawdzić, czy połączenie działa za pomocą komendy “./fastboot devices”. Telefon powinien być widoczny. 

Teraz moment, który był dla mnie problematyczny (https://github.com/aimindseye/hisense-a9/blob/main/unlockbootloader.md) 

, 

#In first window, enter following command  

adb reboot bootloader (if using Linux, use ./adb) 

In second window, enter following commands  

To verify the Fastboot connection, type in the below command and you should get back the device ID. 

fastboot devices(if using Linux, use ./fastboot) 

Note 

If you are not getting any serial ID, then please install the Fastboot Drivers. Before proceeding further 

 

fastboot Hisense unlock (if using Linux, use ./fastboot) 

fastboot erase avb_custom_key (if using Linux, use ./fastboot) 

Ja miałem problem z powyższą komendą - nie wiem, czy wina kabla, czy trzeba, szybko jedną komendę po drugiej 

 

fastboot continue (if using Linux, use ./fastboot) 

Phone will reboot and display a message in Chinese (or in English?) to confirm a complete data wipe. (Press Volume Up and wait.) Confirm using button od display. 

Once phone restarts, you will need to setup phone again. 

To confirm if bootloader is unlocked, goto Settings> System & Updates > Developer Options. Option: OEM unlocking will be grayed out (, there will be "Bootloader is already unlocked") 

D 

Next again enable “usb debugging” 

Authenticate connection 

And reboot: adb reboot bootloader 

fastboot flash boot boot.img 

fastboot flash vbmeta --disable-verity --disable-verification vbmeta.img 

fastboot continue (if using Linux, use ./fastboot) 

Be happy with root 

 
Strony do porównania 

https://www.reddit.com/r/eink/comments/16tpr96/guide_how_to_root_the_hisense_a9/?rdt=34106 

 
https://github.com/aimindseye/hisense-a9/blob/main/rootphone.md

https://github.com/aimindseye/hisense-a9/tree/main
# Unlock Bootloader


> [!WARNING]
> Please proceed at your own risk. There are chances that performing below instructions could lead to unrecoverable phone.
The author is not responsible for any damage caused to the phone with below instructions. 

## Pre-requisites
- ADB Downloaded and in System Path
- Developer Options and USB Debugging Enabled
> [!IMPORTANT]
> **Custom Fastboot downloaded**
- Phone connected via USB ;)


## Steps to Unlock Bootloader (using Windows as OS)

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
