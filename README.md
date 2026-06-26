# pCloudy Release Artifacts

This repository distributes the official CLI tools and automation artifacts for the [pCloudy](https://www.pcloudy.com) device cloud platform.

---

## Repository Structure

```
pcloudy-release-artifacts/
├── android/
│   ├── espresso/          # Espresso automation runner JAR + config
│   └── qconnect/          # QConnect binaries for local device tunnel (Android)
├── ios/                   # iOS artifacts (coming soon)
└── common/                # Shared/cross-platform artifacts (coming soon)
```

---

## Android

### Espresso Automation

Run Espresso tests on pCloudy devices directly from your local terminal using the pre-built JAR runner.

#### Downloads

| File | Description | Direct Download |
|------|-------------|-----------------|
| `pcloudy_espresso.jar` | Espresso runner JAR | [Download](https://raw.githubusercontent.com/Smart-Software-Testing-Solutions-Opkey/pcloudy-release-artifacts/feat/update-new-release-artifacts/android/espresso/pcloudy_espresso.jar) |
| `config.json` | Configuration template | [Download](https://raw.githubusercontent.com/Smart-Software-Testing-Solutions-Opkey/pcloudy-release-artifacts/feat/update-new-release-artifacts/android/espresso/config.json) |

#### Setup & Usage

**Step 1 — Download both files and place them in the same directory**

```
your-folder/
├── pcloudy_espresso.jar
└── config.json
```

**Step 2 — Configure `config.json`**

Open `config.json` in any text editor and fill in the required values across four sections:

```json
{
  "pCloudyConfiguration": {
    "cloudSettings": {
      "endpoint": "https://<your-subdomain>.pcloudy.com/",
      "authentication": {
        "username": "<your-email>",
        "apiKey": "<your-api-key>"
      }
    },
    "testExecution": {
      "durationInMinutes": 10,
      "deviceFullName": ["<DEVICE_FULL_NAME>"],
      "testCycleName": "<your-test-cycle-name>"
    },
    "applicationFiles": {
      "apkFilePath": "<path-to-app.apk>",
      "testApkPath": "<path-to-test.apk>",
      "orchestratorApkPath": "<path-to-orchestrator.apk>",
      "serviceApkPath": "<path-to-service.apk>"
    },
    "testSettings": {
      "suites": [],
      "testRunner": "androidx.test.runner.AndroidJUnitRunner",
      "clearPackageData": false,
      "appPermissionGrant": true,
      "appUpload": true
    }
  }
}
```

| Field | Description |
|-------|-------------|
| `endpoint` | Your pCloudy cloud URL |
| `username` | Your pCloudy account email |
| `apiKey` | Your pCloudy API key (found in account settings) |
| `deviceFullName` | Full device identifier from the pCloudy device list |
| `apkFilePath` / `testApkPath` | Local paths to your app and test APKs |

**Step 3 — Run the JAR**

```bash
java -jar pcloudy_espresso.jar
```

**Step 4 — Monitor live execution**

Once started, pCloudy provides a live view URL in the terminal output. Open it in your browser to watch test execution in real time.

**Step 5 — View the report**

At the end of execution, the terminal prints a direct URL to the full test report.

---

### QConnect — Local Device Tunnel

QConnect lets you connect a pCloudy-reserved device directly to your local machine over ADB. Once connected, the device appears exactly like a locally attached Android device — you can run `adb` commands, install APKs, and use Android Studio against it.

#### Downloads

| Platform | Binary | Direct Download |
|----------|--------|-----------------|
| macOS (Apple Silicon / ARM64) | `QConnect-darwin-arm64` | [Download](https://raw.githubusercontent.com/Smart-Software-Testing-Solutions-Opkey/pcloudy-release-artifacts/feat/update-new-release-artifacts/android/qconnect/QConnect-darwin-arm64) |
| macOS (Intel / AMD64) | `QConnect-darwin-amd64` | [Download](https://raw.githubusercontent.com/Smart-Software-Testing-Solutions-Opkey/pcloudy-release-artifacts/feat/update-new-release-artifacts/android/qconnect/QConnect-darwin-amd64) |
| Linux (AMD64) | `QConnect-linux-amd64` | [Download](https://raw.githubusercontent.com/Smart-Software-Testing-Solutions-Opkey/pcloudy-release-artifacts/feat/update-new-release-artifacts/android/qconnect/QConnect-linux-amd64) |
| Windows (AMD64) | `QConnect-windows-amd64.exe` | [Download](https://raw.githubusercontent.com/Smart-Software-Testing-Solutions-Opkey/pcloudy-release-artifacts/feat/update-new-release-artifacts/android/qconnect/QConnect-windows-amd64.exe) |

#### Prerequisites

- A reserved device session on pCloudy (session ID shown on the device reservation page)
- Your pCloudy account email and API access key
- ADB installed locally (`adb version` to verify)

#### Usage

**Step 1 — Make the binary executable (macOS / Linux)**

```bash
# macOS Apple Silicon
chmod +x ./QConnect-darwin-arm64

# macOS Intel
chmod +x ./QConnect-darwin-amd64

# Linux
chmod +x ./QConnect-linux-amd64
```

**Step 2 — Connect to your reserved device**

```bash
./QConnect-darwin-arm64 connect <SESSION_ID> \
  --email="<your-email>" \
  --access-key="<your-api-key>" \
  --cloud-url="https://<your-subdomain>.pcloudy.com"
```

Replace the placeholders:

| Placeholder | Where to find it |
|-------------|-----------------|
| `<SESSION_ID>` | Shown on the pCloudy device reservation page (e.g. `3700239`) |
| `<your-email>` | Your pCloudy login email |
| `<your-api-key>` | Your pCloudy API key |
| `<your-subdomain>.pcloudy.com` | Your pCloudy cloud URL |

**Example (macOS Apple Silicon)**

```bash
chmod +x ./QConnect-darwin-arm64
./QConnect-darwin-arm64 connect 3700239 \
  --email="user@example.com" \
  --access-key="your_api_key_here" \
  --cloud-url="https://app.pcloudy.com"
```

**Step 3 — Verify the ADB connection**

After the tunnel is established, the terminal will display the ADB address (e.g. `tunnel-stg.pcloudy.com:5574`). Connect via ADB:

```bash
adb connect tunnel-stg.pcloudy.com:5574
adb devices
```

The device will now appear in `adb devices` as if it were physically connected to your machine.

**Windows**

On Windows, run the `.exe` directly from PowerShell or Command Prompt — no chmod needed:

```powershell
.\QConnect-windows-amd64.exe connect <SESSION_ID> --email="<your-email>" --access-key="<your-api-key>" --cloud-url="https://<your-subdomain>.pcloudy.com"
```

---

## iOS

> Coming soon — iOS artifacts will be added here.

---

## Common

> Coming soon — shared/cross-platform artifacts will be added here.

---

## Support

For issues or questions, contact the pCloudy support team or refer to the [pCloudy documentation](https://www.pcloudy.com/docs).
