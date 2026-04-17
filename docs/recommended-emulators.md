Last updated: {{ git_revision_date_localized }}


## Recommended Emulators

These are common Windows emulators that should work well for this guide. Pick whichever one you are most comfortable with and follow the emulator-specific notes below.

| Emulator | Link | Specific instructions |
| --- | --- | --- |
| **BlueStacks 5** | [HERE](https://www.bluestacks.com/) | The most used one so far by the testers, has built in controls mapping, almost no ads.|
| **MuMu Player** | [HERE](https://www.mumuplayer.com/en/) | Install `patched_aligned.apk` with drag and drop or the built-in **APK** button. If you need `adb`, open **Device Diagnostic** or **ADB port** in the emulator menu to see the localhost port, then connect from your PC with `adb connect 127.0.0.1:<port>`. |
| **LDPlayer** | [HERE](https://www.ldplayer.net/) | Install `patched_aligned.apk` by dragging it into the emulator window or by clicking **Install APK** on the right toolbar. If drag and drop does not trigger, use the toolbar import option instead. |

## Notes

- The installation guide assumes the emulator is running on the same PC as the server.
- Keep the server running before launching the game inside the emulator.
- If one emulator gives you trouble, it is often faster to try a different one than to keep fighting a broken instance.
