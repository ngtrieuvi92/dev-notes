# Rasberry Pi 4B - Bookworm HDMI config

Add lines below into the end of /boot/firmware/config.txt

```
hdmi_force_hotplug=1
hdmi_group=1
hdmi_mode=1
hdmi_drive=2
```

Reboot device
