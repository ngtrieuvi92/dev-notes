# Cloudflare warp multiple org

Sample plist config for multiple org setup

```bash
sudo vi /Library/Managed Preferences/com.cloudflare.warp.plist
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN">
  <plist version="1.0">
  <dict>
    <key>configs</key>
    <array>
      <dict>
        <key>organization</key>
        <string>org1</string>
        <key>display_name</key>
        <string>Org1</string>
      </dict>
      <dict>
        <key>organization</key>
        <string>org2</string>
        <key>display_name</key>
        <string>Org2</string>
      </dict>
    </array>
  </dict>
  </plist>
```
