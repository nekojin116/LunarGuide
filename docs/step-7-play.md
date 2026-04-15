## Step 7 — Install and Play

### Android phone or tablet (not tested personally)

Install the Tailscale app from the Play Store (see [Tailscale Setup](#tailscale-setup)), then install the patched APK:

```bash
adb install patched.apk
```

Or transfer `patched.apk` to your phone and tap to install.

### Android emulator (BlueStacks, LDPlayer, etc.)

Drag and drop `patched.apk` onto the emulator window, or:

```bash
adb connect 127.0.0.1:<emulator-adb-port>
adb install patched.apk
```

Since the emulator runs on the same PC as the server, Tailscale isn't required for home use.

> If you're using the emulator on a **different PC away from home**, install Tailscale on that PC and it will route through automatically.

### Make sure the server is running before launching the game.
