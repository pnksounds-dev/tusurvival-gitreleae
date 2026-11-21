# tusurvival-gitreleae

Public release host for **TU // ZOMBIE SURVIVAL** — the free Android build of
[TU-Survival](https://survival.terraunbound.co.uk). The code repo is private;
this repo exists so GitHub can serve release assets anonymously.

## What lives here

Nothing but releases. Each `v*` release carries the same signed APK twice:

| Asset | Purpose |
| --- | --- |
| `TU-Zombie-v<major>.<minor>.<patch>.<versionCode>.apk` | In-app self-updater — the app parses `versionCode` off the filename and compares it to the installed build. **Keep this exact name.** |
| `tu-zombie-survival.apk` | Stable direct-download link for the website. |

## Stable download link

`https://github.com/pnksounds-dev/tusurvival-gitreleae/releases/latest/download/tu-zombie-survival.apk`

GitHub's `latest` redirect always serves the newest release's copy — this URL
never changes. It's what the browser build's ANDROID APP button and ON
MOBILE? prompt point at.

## Install

1. Download the APK on the phone (link above).
2. Android asks to allow installs from the browser/source — grant it.
3. Open the APK, install. Signed `CN=PNK Sounds` with the
  `tu-zombie-upload` key — updates must carry the same signature or Android
  refuses them.
4. After this first install the app updates itself: an UPDATE AVAILABLE card
   shows in the main menu when a newer release exists.

## Cutting a release (maintainer notes)

```bash
# in ../TU-survival — commit first, versionCode = git rev-list --count HEAD
npm run android:sync && npm run android:apk

gh release create v<versionName> \
  android/app/build/outputs/apk/release/TU-Zombie-v<name>.<code>.apk \
  "android/app/build/outputs/apk/release/TU-Zombie-v<name>.<code>.apk#tu-zombie-survival.apk" \
  --repo pnksounds-dev/tusurvival-gitreleae --title "TU // ZOMBIE SURVIVAL v<versionName>"
```

Bare `v*` tags only — `releases/latest` resolution and semver sorting depend
on it. Never rename the versioned asset; the updater's regex is
`^TU-Zombie-v(\d+)\.(\d+)\.(\d+)\.(\d+)\.apk$`.
