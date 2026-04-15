## Step 4 — Patch the APK

This rewires the game app to connect to your PC instead of the dead official servers.

### 4a. Get your Tailscale IP (Skip if you are running the game on an emulator)

Before patching, you need your PC's Tailscale IP (see the [Tailscale Setup](#tailscale-setup) if you haven't done that yet). It looks like `100.x.x.x`. Find it via the Tailscale tray icon or:

```bash
tailscale ip
```

### 4b. Decompile the APK

```bash
apktool d "NieR Re[in]carnation 3.7.1.apk" -o patched
```

### 4c. Run the patcher

Replace `100.x.x.x` with :
 - For Tailscale users : Tailscale IP
 - For Emulator users : 10.0.2.2

```bash
python3 lunar-scripts/patch_apk.py patched --server-ip 100.x.x.x --http-port 8080
```

### 4d. Rebuild the APK

```bash
apktool b patched -o patched.apk
```

### 4e. Generate a signing key (one-time only)

Skip this if you already have `debug.keystore`.

```bash
keytool -genkeypair -v 
  -keystore debug.keystore 
  -alias androiddebugkey 
  -storepass android -keypass android 
  -keyalg RSA -keysize 2048 -validity 10000 
  -dname "CN=Android Debug,O=Android,C=US"
```

### 4f. Sign the APK

```bash
apksigner sign --ks debug.keystore --ks-pass pass:android patched.apk
```

You now have `patched.apk` ready to install.
