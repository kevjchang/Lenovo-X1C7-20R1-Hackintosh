# Lenovo-X1C7-20R1-Hackintosh
MacOS Opencore EFI configuration for Lenovo Thinkpad X1 Carbon (7th Gen)

Using Opencore 8.9, booting MacOS Monterey

This repo serves as a reference/guide for beginners with the same/similar hardware as me (optimally same CPU and iGPU). Check out the much better documented X1C7 repos for a more thorough explanation on why certain kexts were used and why certain features will not work.


All needed files were gathered by following the Dortania install guide: https://dortania.github.io/OpenCore-Install-Guide/

The EFI folder was built (basically) from scratch using only the official opencore guide, so this should be a very minimally bloated setup for booting Monterey.

To use the EFI folder in your own USB, you will need to properly format the USB and add the Monterey recovery image (shown here) https://dortania.github.io/OpenCore-Install-Guide/installer-guide/windows-install.html   <-- Follow this guide to the end of the webpage.

Then simply replace the default EFI folder that Opencore provides with my EFI folder, which adds a bunch of necessary kext files and removes unneeded drivers.

Afterwards, you will need to update SMBIOS values to generate a valid serial number so that services such as iMessage will work. The link below will instruct you to download a program called GenSMBIOS to generate these values, and show you how to insert them. My config.plist file has been filled with random serial number and ROM values, so you will need to replace those.

I used MacBookPro16,3 as the base model to general serial numbers off of.

https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake-plus.html#platforminfo

To insert the values properly into the config.plist file, I used propertree. https://github.com/corpnewt/ProperTree


**My hardware specs:**

Model: 20R1

CPU: Intel Core i5-10210U (formerly Comet Lake)

iGPU: Intel UHD Graphics for Comet Lake

SSD: WDC PC SN730 SDBQNTY-256G-1001

RAM: 8GB DDR3 (or something like that)

Audio: Realtek ALC285

Wifi: Intel Wireless-AC 9560 160MHz Wireless Network Adapter

Ethernet: Intel 82574IT Gigabit Ethernet Controller

Initially, the UHD graphics were not being used by MacOS due to an error in my config. 
- integrated graphics support was enabled by modifying my original config file using values from: https://elitemacx86.com/threads/how-to-enable-intel-uhd-graphics-comet-lake-on-macos-big-sur-and-later.897/

REMINDER: This setup will likely not install MacOS for you unless you are using the exact same CPU model (WITH SAME iGPU), bios settings, and MacOS version. So please use this only as a reference.

Wifi, and most essentials should be working (haven't fully tested)
- Audio setup is not making full use of the speakers, so audio quality is noticeably worse (but still usable). The audio setup can be changed by changing the alcid value in config.plist, haven't yet tested other audio arrangements so I don't know how much better/worse the audio could be adjusted.

Working:
- Wifi/Bluetooth
- Sidecar (only when connected through cable, with thunderbolt enabled in bios security settings)
- Apple services (must generate valid SMBIOS first)
- HDMI port (However it takes longer to connect to external display than on Windows 11, and disconnecting HDMI causes the laptop display to go black for 1-2 minutes before resuming normal function)

What isn't working:
- Airdrop (will probably need to switch wifi/bluetooth card. If bluetooth card is swapped, wireless sidecar should also work)
- Fingerprint reader
- Microphone


Uploaded Opencore bootloader is in release mode. I suggest downloading the debug version of Opencore and replacing the config.list, ACPI, Kext, and Driver files (except OpenCanopy.efi) with mine if you are installing for the first time.

To successfully enable dual boot using opencore, you must set LauncherOption to "Full" in config.plist, reset NVRAM, and boot into MacOS once to create the opencore boot path in BIOS. Once that has been done, mount the efi (see the official opencore post-install guide for more info) and you can then partition and install Windows/other OSes onto the same drive.
