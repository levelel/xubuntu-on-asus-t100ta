# Update for xubuntu 21.04 on T100TA

The latest xubuntu (21.04) works out of the box for most of the issues listed. Namely, numlock, touch screen, backlit control, HDMI, sound, and Wifi will work without any tweaks, which is awesome!

## Notes:

### DO download the amd64 version of xubuntu, as 32 bit version won't install.

### Mount /target
At the step of bootloader installation -> chroot, /target is not mounted by default, you have to manually do it by `mount /dev/mmcblk2p2 /target`

### Modify the boot screen
The boot screen is called GRUB. The process of modifying the GRUB menu is kind of vague in the original guide. Here are some tweaks.

The configurations of GRUB is located in the file `/etc/default/grub`. There is no `/boot/efi/grub/grub.cfg` file.

So in order to change the boot menu settings, just `sudo nano /etc/default/grub` and change whatever you want in the file.

### Fix for unstable Wifi
Wifi disconnects and asks for password again and again quite frequently if your wifi is in WPA2/WPA3 mixed mode.

The reason for that problem is that WPA3 doesn't authenticate on the machine. And the system will recognize the Wifi signal as two separate ones, one for WPA2, and the other for WPA3. For example, my wifi SSID is called "my_wifi", and is mixed WPA2/WPA3 Personal. Xubuntu will connect to "my_wifi" with WPA2, but when it disconnects, it keeps trying to connect to the same SSID using WPA3 for some reason. And in this situation, the WPA3 version of the same wifi connection would appear as "my_wifi1" (note that there is a number "1" appended") in the connection list. Xubuntu would keep asking for password when it tries to connect with WPA3 and authentication would always fail.

Solution: the solution is to disable auto-connect for the WPA3 connection. Click the connection icon in the taskbar at the top-right corner. Then click "Edit Connections", find the WPA3 connection by checking the Wi-Fi Security tab, and uncheck "Connect automatically with priority xx" in General tab.