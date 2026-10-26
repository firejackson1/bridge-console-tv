# Bridge Console TV 0.60 — Public Preview

First public preview of the LCARS-inspired Android TV launcher.

- Ten whole-screen LCARS layouts plus the classic layout.
- Unified Orbital app slices, clear focus and directional navigation guide.
- Animated starfields, screensaver, palettes and console lights.
- App pinning, folders, search and recent apps.
- Optional Home Assistant controls: compact reveal, then full popup on the next press.

## Install

Download **BridgeConsoleTV.apk** from Assets, transfer it to your Android TV and open it using a file manager or browser. Allow installs from that application if Android requests it. Android TV 8.0 or newer is required. Test the launcher before changing your default Home app; available defaults vary by TV.

**Development-build migration:** This public APK uses a dedicated release signing key. Existing development-signed installations cannot update to it in place. Export settings before switching; uninstalling can remove data. Future public releases will retain this public signing identity.

## Verification and limits

The underlying 0.60 development build passed 3,198 host checks and 1,064 native device checks on onn 4K Pro, including Orbital navigation, settings and Home Controls. Public release signature and checksum are separately verified. The public-key APK has not been installed over the owner's development build. Short frame samples do not establish sustained/all-speed performance. Other TV devices and third-party widget providers can differ.

Optional Home Assistant setup and notification access are configured locally; the APK contains no owner account configuration. See **SHA256SUMS.txt**, **third-party-notices.txt** and **Antonio-OFL.txt** in Assets.

Unofficial fan project; not affiliated with or endorsed by Star Trek or its owners. Support is optional. The [download page](https://firejackson1.github.io/bridge-console-tv/#support) includes a PayPal donation button.

## Layout screenshots

[Browse all eleven layouts](https://firejackson1.github.io/bridge-console-tv/#layouts), or download **BridgeConsoleTV-layout-screenshots.zip** from Assets. Native captures use a temporary arrangement of separately installed media apps; no storage or Jackson Lab store/camera apps appear.

## Set as Home on onn

See the [onn default-launcher guide](https://github.com/firejackson1/bridge-console-tv/blob/main/ONN-SETUP.md) for the built-in chooser, ADB connection and Home-setting commands, verification, undo and the tvQuickActions alternative.
