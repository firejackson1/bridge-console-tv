# Bridge Console TV

A free LCARS-inspired Android TV launcher. Early public preview.

**[Download page](https://firejackson1.github.io/bridge-console-tv/)** · **[APK and release notes](https://github.com/firejackson1/bridge-console-tv/releases)** · **[Report an issue](https://github.com/firejackson1/bridge-console-tv/issues)**

![Actual Orbital layout](images/layout-03.png)

Ten LCARS layouts plus a classic layout, an app drawer in every layout, animated starfield backgrounds/screensaver, app organization and optional Home Assistant controls. Android TV 8.0 or newer; tested on onn 4K Pro.

Read installation instructions and development-signing migration notes on the download page. This repository hosts the public page and releases, not the development source history. No signing keys, credentials or device configuration are published here.

Support is optional. Use the PayPal button on the [download page](https://firejackson1.github.io/bridge-console-tv/#support) if you would like to support development.

Unofficial fan project; not affiliated with or endorsed by Star Trek or its owners. Antonio is licensed under the SIL Open Font License; see licenses/Antonio-OFL.txt. APK third-party notices accompany each release.

## All layouts

[View the complete native screenshot gallery](https://firejackson1.github.io/bridge-console-tv/#layouts). The ten LCARS layouts and classic bridge use an arranged set of separately installed media apps.

![Vertical Pylons](images/layout-06.png)

![Hybrid Bridge](images/layout-10.png)

## Set as the Home launcher on onn

1. Open Bridge **Settings → Android & device → Choose default home app** and select Bridge Console TV if Android offers the chooser.
2. If it is unavailable, connect ADB to your own box and save the existing Home component before changing it.
3. Set the owner-user Home activity, then verify with Android's resolver and test the physical Home button:

```sh
adb -s TV_ADDRESS shell cmd package set-home-activity --user 0 lab.jackson.lcars/.MainActivity
adb -s TV_ADDRESS shell cmd package resolve-activity --brief -a android.intent.action.MAIN -c android.intent.category.HOME
```

Replace `TV_ADDRESS` with your own `adb devices` entry. **[Full onn guide: connection, backup, verification, undo and tvQuickActions alternative](ONN-SETUP.md).** Home-button remapping is a workaround and is not the same as changing Android's registered default launcher. Keep your original launcher installed.
