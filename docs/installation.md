# Installation

## Step 1 — Prepare the Asset Folders

Open your terminal in cage/

Create the required folders and copy the master data binary into place:

```bash
mkdir -p lunar-tear/server/assets/release
mkdir -p lunar-tear/server/assets/master_data
mkdir -p lunar-tear/server/assets/revisions
```

Copy/move the `.bin.e` into the release folder (keep the original at the `cage` root untouched).

Extract `resource_dump_android.7z` into `lunar-tear/server/assets/revisions/`. 

Note : Only *Revision 0* is necessary currently so only extract folder 0 to save on space 

---

## Step 2 — Dump the Master Data

This decrypts the `.bin.e` and converts it into JSON files the server can read. Column names are resolved automatically from `lunar-scripts/schemas.json` — no external dependencies needed.

To avoid an issue with Unicode, run this line first :

```bash
$env:PYTHONUTF8 = 1
```

```bash
python3 lunar-scripts/dump_masterdata.py  --input lunar-tear/server/assets/release/20240404193219.bin.e --output lunar-tear/server/assets/master_data
```

When done, `lunar-tear/server/assets/master_data/` should be filled with `EntityM*.json` files.

---

## Step 3 — Patch the Master Data

This extends all content expiry dates inside the `.bin.e` so events, quests, and banners don't show as expired. It also empties the maintenance table so the game never shows a maintenance screen.

```bash
python3 lunar-scripts/patch_masterdata.py  --input lunar-tear/server/assets/release/20240404193219.bin.e
```

---

## Step 4 — Patch the APK

This rewires the game app to connect to your PC instead of the dead official servers.

### 4a. Get your Tailscale IP (Skip if you are running the game on an emulator)

Before patching, you need your PC's Tailscale IP (see the [Tailscale Setup](tailscale-setup.md) if you haven't done that yet). It looks like `100.x.x.x`. Find it via the Tailscale tray icon or:

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

---

## Step 5 — Generate Server Code (one-time)

```bash
cd lunar-tear/server
make proto
```

This generates Go code from the `.proto` files. Only needs to be done once.

---

## Step 6 — Run the Server

```bash
cd lunar-tear/server
go run ./cmd/lunar-tear --host 100.0.2.2 --http-port 8080 --scene 0
```

Use `--scene x` argument to skip over the undesired content.

> **Important:** The server only saves your progress when you advance to a new story scene. Gacha pulls, purchases, and enhancements done between scene transitions are lost if the server shuts down before you reach the next checkpoint. This is a current limitation of the server.

Leave the terminal open — the server must keep running while you play.

---

## Step 7 — Install and Play

### Android phone or tablet (not tested personally)

Install the Tailscale app from the Play Store (see the [Tailscale Setup](tailscale-setup.md)), then install the patched APK:

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
