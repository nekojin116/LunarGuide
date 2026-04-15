## Android Build Tools

Necessary tools for APK patching (`apksigner`, `zipalign`)

### Installation

1. Visit [Android Studio](https://developer.android.com/studio) and scroll down to the `Command line tools only` section.

2. Download the **Windows Package**.

    ![](images/cmd_windows.png)

3. Extract the downloaded archive. The directory structure should look like this:

        root/
            cmdline-tools/
                bin/
                    sdkmanager.bat ← download tool
            ...

4. Inside `cmdline-tools`, create a subfolder `latest`:

        root/
            cmdline-tools/
                latest/
                    bin/
                        sdkmanager.bat ← download tool
                    ...

5. Open your terminal in `bin/`.

6. Run the following command to install the required build tools:

    ```
    sdkmanager.bat "build-tools;34.0.0"
    ```

7. If you are using a newer Java version (e.g., 21 or later), you may encounter the warning:

    ```
    Java version 17 or higher is required
    ```

    To bypass the version check, run:

    ```
    set SKIP_JDK_VERSION_CHECK=true
    ```

    Then re-run the previous `sdkmanager` command.

8. When prompted, accept the license agreement by entering `y`.

9. After installation completes, `apksigner` and `zipalign` will be located in:
   
        root/
            .temp/
            cmdline-tools/
                latest/
                    bin/
                        sdkmanager.bat
            build-tools/
                34.0.0/
                    apksigner.bat
                    zipalign.exe
            licenses/

### Optional: Add Build Tools to Environment Variables

1. Add `<root>/build-tools/34.0.0` to **Environment Variables**.

2. Press `Win + S` and search for **Environment Variables**.

3. Click **Edit the system environment variables**.

4. In the System Properties window, click **Environment Variables…**

5. Under **System variables**, find and select `Path`, then click **Edit**

6. Click **New** and add the full path to your build-tools folder (replace `<root>` with your actual path): `<root>\build-tools\34.0.0`

7. Click **OK** on all windows to save.

8. Close and reopen your terminal (CMD / PowerShell / Terminal).

9. Run the following commands to verify:

        zipalign
        apksigner



