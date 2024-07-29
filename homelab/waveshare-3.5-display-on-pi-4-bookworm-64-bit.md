# Waveshare 3.5" display on Pi 4 -Bookworm 64 Bit



Source: [https://www.waveshare.com/wiki/3.5inch\_RPi\_LCD\_(C)\_Manual\_Configuration#For\_Bookworm\_System](https://www.waveshare.com/wiki/3.5inch\_RPi\_LCD\_\(C\)\_Manual\_Configuration#For\_Bookworm\_System)&#x20;

### For Raspberry Pi 4 & Raspberry Pi 5

#### Download and Compile fbcp

Open the Raspberry Pi terminal and execute:

```
sudo apt install libraspberrypi-dev -y
sudo apt-get install unzip -y
sudo apt-get install cmake -y
sudo wget https://files.waveshare.com/upload/1/1e/Waveshare35c.zip
sudo unzip ./Waveshare35c.zip
sudo cp waveshare35c.dtbo /boot/overlays/
sudo wget https://files.waveshare.com/upload/1/1e/Rpi-fbcp.zip
sudo unzip ./Rpi-fbcp.zip
cd rpi-fbcp/
sudo rm -rf build
sudo mkdir build
cd build
sudo cmake ..
sudo make -j4
sudo install fbcp /usr/local/bin/fbcp
```

Edit "config.txt" file:

```
sudo nano /boot/firmware/config.txt
```

Blocking the following sentence:

[![FBCP CLOSE.jpg](https://www.waveshare.com/w/upload/3/38/FBCP\_CLOSE.jpg)](https://www.waveshare.com/wiki/File:FBCP\_CLOSE.jpg)

Add the following code at the end of config.txt:

```
dtparam=spi=on
dtoverlay=waveshare35c
hdmi_force_hotplug=1
max_usb_current=1
hdmi_group=2
hdmi_mode=1
hdmi_mode=87
hdmi_cvt 480 320 60 6 0 0 0
hdmi_drive=2
display_rotate=0
```

#### Set Auto-start startx and fbcp

* Open ".bash\_profile". If there is no ".bash\_profile" file, you can create one:

```
sudo nano ~/.bash_profile
```

Add the following code at the bottom of the ".bash\_profile" file:

```
if [ "$(cat /proc/device-tree/model | cut -d ' ' -f 3)" = "5" ]; then
    # rpi 5B configuration
    export FRAMEBUFFER=/dev/fb1
    startx  2> /tmp/xorg_errors
else
    # Non-pi5 configuration
    export FRAMEBUFFER=/dev/fb0
    fbcp &
    startx  2> /tmp/xorg_errors
fi
```

* Open the "99-fbturbo.\~" file, if it exists, you need to check fb is "fb0":

```
sudo nano /usr/share/X11/xorg.conf.d/99-fbturbo.~
```

Add the following code in the "99-fbturbo.\~" file:

```
Section "Device"
        Identifier      "Allwinner A10/A13 FBDEV"
        Driver          "fbturbo"
        Option          "fbdev" "/dev/fb0"

        Option          "SwapbuffersWait" "true"
EndSection
```

#### Set CLI Auto-login

```
sudo raspi-config nonint do_boot_behaviour B2
sudo raspi-config nonint do_wayland W1
sudo reboot
```

After rebooting, the main screen can normally display.\
Note 1: Please ensure the username of the Raspberry Pi is "pi", otherwise, it cannot automatically log in.\
Note 2: After setting the above configuration, it may take a while to reboot the system and load SSH.

#### Configure Touch

* Install calibrator software:

```
sudo apt-get install xserver-xorg-input-evdev 
sudo cp -rf /usr/share/X11/xorg.conf.d/10-evdev.conf /usr/share/X11/xorg.conf.d/45-evdev.conf
sudo apt-get install xinput-calibrator
```

* Edit 99-calibration.conf configuration file:

```
sudo nano /usr/share/X11/xorg.conf.d/99-calibration.conf
```

Add the following content to the "99-calibration.conf" configuration file:

```
Section "InputClass"
        Identifier      "calibration"
        MatchProduct    "ADS7846 Touchscreen"
        Option  "Calibration"   "3932 300 294 3801"
        Option  "SwapAxes"      "1"
        Option "EmulateThirdButton" "1"
        Option "EmulateThirdButtonTimeout" "1000"
        Option "EmulateThirdButtonMoveThreshold" "300"
EndSection
```

Reboot to take effect.\


```
sudo reboot
```
