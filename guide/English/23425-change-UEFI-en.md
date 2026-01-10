<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">

# Running Silicium UEFI on Xiaomi pad 5

## Installation

### Prerequisites
- ```Installed Windows```

-  ```Brain```

- ```Windows 10(or higher) PC/Laptop```

- [```New UEFI```](https://t.me/siliciumnabu/))

- [```DriveLetterAssigner Tool```](https://github.com/Misha803/My-Scripts/releases/tag/DriveLetterAssigner)

- [```Android platform tools```](https://developer.android.com/studio/releases/platform-tools)

- [```Modified recovery image```](https://github.com/ArKT-7/twrp_device_xiaomi_nabu/releases/tag/mod-win)

### Opening CMD as an administrator
> [!NOTE]
> Don't know how to start? Unzip the downloaded [```Android platform tools```](https://developer.android.com/studio/releases/platform-tools), then open ```command prompt``` as an administrator and run the following command, replacing `"path\to\platform-tools"` with the actual path of the platform tools folder
```cmd
cd "path\to\platform-tools"
```
> Use this window throughout the entire guide. Do not close it.

> [!Note]
> If your device is not detected in fastboot or recovery mode, you'll have to install USB drivers [using this guide](troubleshooting-en.md#device-is-not-recognized-in-fastboot-or-recovery)

#### Reboot into fastboot mkde
- Boot your NABU into **fastboot mode** by holding down the **`volume down`** button while rebooting with a USB cable connected
- Alternatively, run the below command while booted in Android
```cmd
adb reboot bootloader
```

### Boot the modded recovery
> While in fastboot mode, replace `path\to\recovery.img` with the actual path of the recovery image
```cmd
fastboot boot path\to\recovery.img
```

### Assign letters to WINNABU and ESPNABU
> Run the **DriveLetterAssigner** and click **`YES`** to automatically assign the letters **X** and **Y** to **WINNABU** and **ESPNABU**

#### Enabling test signing
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Disabling recovery
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Disabling integrity checks
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

#### Remove the drive letter for ESP
> If this does not work, ignore it and skip to the next command. This phantom drive will disappear the next time you reboot your PC.
```cmd
mountvol y: /d
```

### Reboot to fastboot
```cmd
adb reboot bootloader
 ```


#### Boot into the UEFI
> Replace `path\to\mu-nabu` with the actual path of the UEFI image
```cmd
fastboot boot path\to\mu-nabu.img
```

#### [Last step: Setting up dualboot](/guide/English/dualboot-selection-en.md)

</details>

----


































