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
