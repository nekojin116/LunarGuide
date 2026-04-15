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

Use `--scene x`  argument to skip over the undesired content.

> **Important:** The server only saves your progress when you advance to a new story scene. Gacha pulls, purchases, and enhancements done between scene transitions are lost if the server shuts down before you reach the next checkpoint. This is a current limitation of the server.

Leave the terminal open — the server must keep running while you play.
