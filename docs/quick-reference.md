## Quick Reference

```
One-time setup:
  pip install pycryptodome msgpack lz4
  go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
  go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
  cd lunar-tear/server && make proto
  keytool -genkeypair ...   (generates debug.keystore at `cage` root)

Prepare assets (first time):
  cp 20240404193219.bin.e lunar-tear/server/assets/release/
  7z x resource_dump_android.7z -o lunar-tear/server/assets/revisions/
  python3 lunar-scripts/dump_masterdata.py \
    --input lunar-tear/server/assets/release/20240404193219.bin.e \
    --output lunar-tear/server/assets/master_data
  python3 lunar-scripts/patch_masterdata.py \
    --input lunar-tear/server/assets/release/20240404193219.bin.e

Patch APK (first time or if server IP changes):
  apktool d "NieR Re[in]carnation 3.7.1.apk" -o patched
  python3 lunar-scripts/patch_apk.py patched --server-ip 100.x.x.x --http-port 8080
  apktool b patched -o patched.apk
  apksigner sign --ks debug.keystore --ks-pass pass:android patched.apk
  adb install patched.apk

Run server (first time):
  cd lunar-tear/server
  go run ./cmd/lunar-tear --host 100.x.x.x --http-port 8080 --scene 13

Run server (resuming — check snapshots/ for latest scene number):
  cd lunar-tear/server
  go run ./cmd/lunar-tear --host 100.x.x.x --http-port 8080 --scene <latest>
```
