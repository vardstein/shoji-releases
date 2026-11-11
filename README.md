# Shōji releases

Signed APKs of Shōji 障子, a calm home screen for Android tablets and phones (Android 10 and up),
and of Shōji Weather, its optional weather add-on. This repo holds builds only. The source is not
public.

Every release carries both apps:

| File | App | Install id |
|---|---|---|
| `shoji-<version>.apk` | Shōji, the home screen | `de.openjade.shoji` |
| `shoji-weather-<version>.apk` | Shōji Weather, fetches the weather for Shōji | `de.openjade.shoji.weather` |

Shōji itself has no internet permission. Only the add-on goes online, and only if you set it up.

## Install with Obtainium

Add this repo once for each app you want.

Shōji:

1. Add app, source URL `https://github.com/vardstein/shoji-releases`
2. Releases are named `v1.0.0`. For test builds too, turn on "Include prereleases" (builds from
   dev are pre-releases named `v1.0.1-dev.N`)
3. Under "Filter APKs by regular expression" put `^shoji-\d`
4. Add, then Install. To make it the home screen, open Shōji settings and tap "Make Shōji the home
   screen"

Shōji Weather (optional):

1. Add app again, same source URL
2. Turn on "Include prereleases"
3. Under "Filter APKs by regular expression" put `^shoji-weather-`
4. Add, then Install. Pick a weather source in Shōji settings under Weather

## Check the signature

Both APKs are signed with this certificate (SHA-256):

```
53:D7:3C:B1:41:FA:BC:12:1A:F4:71:B9:2B:C5:1B:3E:76:43:AB:3A:84:24:9A:8A:34:73:5E:DB:94:B8:16:70
```

`apksigner verify --print-certs shoji-*.apk` must show the same digest. Android refuses an update
signed with another key, so a swapped APK can't replace an installed one. The two apps also only
talk to each other when both carry this certificate. Each release lists every APK's own SHA-256.

## How builds get here

Shōji's CI hands each dev build and each release from main over on a branch `incoming/v<version>`. The publish workflow checks
both APKs' SHA-256, package, version and signing certificate against `cert-sha256.txt`, then makes
the release (a pre-release for `-dev` builds) and deletes the branch.
