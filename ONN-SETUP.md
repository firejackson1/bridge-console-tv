# Make Bridge Console TV your Home screen on onn

These instructions are for your own onn Android TV / Google TV box. Firmware and settings menus vary. Install and open Bridge Console TV before changing Home behavior. Keep the original launcher installed.

## 1. Try the built-in home-app chooser

In Bridge Console TV, open **Settings → Android & device → Choose default home app**. Select **Bridge Console TV** and confirm Android's Home-app request if it is offered. Press the remote's Home button to test. If the box does not expose a working chooser or still opens Google TV, use the next method.

## 2. ADB: set Android's registered Home app

This uses Android's package-manager Home setting. It does not require uninstalling or disabling the Google launcher.

### Connect to your own box

1. Download [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools) on your computer. Open a terminal in that folder (PowerShell users may need `./adb` instead of `adb`).
2. On most onn Google TV builds, go to **Settings → System → About → Android TV OS build** and press OK seven times to enable Developer options. Older menus may use Device Preferences → About → Build.
3. Under Developer options, enable the debugging option your box offers and approve the connection on the TV. Your computer and TV should be on the same trusted local network.
4. If **Wireless debugging** offers pairing, use the displayed pairing address/port with `adb pair TV_IP:PAIRING_PORT`, enter the code shown on the TV, then use `adb connect TV_IP:CONNECTION_PORT`. Pairing and connection ports can differ.
5. Some onn firmware instead exposes network ADB after **USB debugging** is enabled. On that firmware, connect using `adb connect TV_IP:5555`. If it refuses the connection, use the debugging method exposed by your firmware rather than guessing ports.
6. Run `adb devices`. In the commands below, replace **TV_ADDRESS** with your own box's exact device entry, such as `192.168.1.50:5555`. Do not use somebody else's TV address.

See [Android's ADB connection documentation](https://developer.android.com/tools/adb) for platform-specific setup.

### Save the current Home component

Run this first and keep the final component line so you can undo the change:

```sh
adb -s TV_ADDRESS shell cmd package resolve-activity --brief -a android.intent.action.MAIN -c android.intent.category.HOME
```

If it reports a resolver rather than one launcher, use the device's chooser to select your preferred original Home app before proceeding.

### Choose Bridge Console TV

```sh
adb -s TV_ADDRESS shell cmd package set-home-activity --user 0 lab.jackson.lcars/.MainActivity
```

`--user 0` targets the usual owner user on onn boxes. If you use a separate Android system user, check `adb -s TV_ADDRESS shell am get-current-user` and substitute that user number.

### Verify

```sh
adb -s TV_ADDRESS shell cmd package resolve-activity --brief -a android.intent.action.MAIN -c android.intent.category.HOME
```

The resolved component should be `lab.jackson.lcars/.MainActivity`. Then test the physical Home button and, when convenient, restart your own TV box and test again. A successful command or resolver result alone does not prove the physical button or boot behavior on every firmware.

If the command fails or your firmware rejects it, keep system launchers in place and use the button-remapping alternative below or report your device/firmware version. Do not follow generic instructions to uninstall Google TV or disable unrelated services.

### Undo

Replace **PREVIOUS_HOME_COMPONENT** with the component you saved earlier:

```sh
adb -s TV_ADDRESS shell cmd package set-home-activity --user 0 PREVIOUS_HOME_COMPONENT
```

Verify with the same resolve command and test Home. Turn off debugging when you no longer need it. These instructions do not require a factory reset or removing the original launcher.

Android's [`set-home-activity` implementation/help](https://android.googlesource.com/platform/frameworks/base/+/refs/heads/main/services/core/java/com/android/server/pm/PackageManagerShellCommand.java) documents the Home-setting command.

## 3. Home-button alternative: tvQuickActions

If you prefer a remote-button approach, install tvQuickActions from its official Play Store listing, follow its accessibility setup, then open **Mappings** (called Buttons & Actions in some versions), add the Home button, choose **Usual action**, and assign **single press → App → Bridge Console TV**. Some buttons require additional setup depending on firmware; follow the developer's instructions if Home cannot be captured.

This remaps the button. It does **not** by itself change Android's registered default Home app, and startup behavior after reboot may still differ. tvQuickActions is a separate third-party app; available features and pricing are set by its developer. See the [official quick-start guide](https://tvdevinfo.com/tvquickactions/quick-start/).

## Home still opens another launcher?

Check whether another launcher or a button-remapping app is intercepting Home. Change only that conflicting Home override or mapping; do not disable all accessibility services or erase other remote shortcuts. An enabled Projectivy Home override, for example, can take precedence over the registered Home selection.

Bridge Console TV was tested on an onn 4K Pro. These instructions do not claim every onn model/firmware is identical. No settings on the developer's TV were changed while preparing this guide.
