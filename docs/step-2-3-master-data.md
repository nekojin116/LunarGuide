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
