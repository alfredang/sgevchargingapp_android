# Google Play submission — SG EV Charging (closed testing)

This guide covers uploading the signed app bundle to **Google Play Console** and
rolling it out to a **closed test** track for review.

> The release **AAB** and all store graphic assets are already built (see below).
> The final upload requires signing in to your Play Console account, which cannot
> be automated headlessly — follow the steps here to finish.

## What's already built

| Artifact | Path |
| --- | --- |
| Signed release bundle | `app/build/outputs/bundle/release/app-release.aab` |
| App icon (512×512) | `play-assets/app-icon-512.png` |
| Feature graphic (1024×500) | `play-assets/feature-graphic-1024x500.png` |
| Phone screenshot 1 | `play-assets/phone-screenshot-1.png` |
| Phone screenshot 2 | `play-assets/phone-screenshot-2.png` |

> The screenshots are accurate UI mockups (1080×1920). For the best listing,
> replace them with real captures from a device/emulator once you have a Google
> Maps API key wired in (`adb exec-out screencap -p > shot.png`).

## Signing

The bundle is signed with `keystore/sgevcharging-release.jks` (NOT committed).
Credentials live in `local.properties` (NOT committed). **Back up the keystore
and passwords** — losing them means you can never update this app again.

```
keystore : keystore/sgevcharging-release.jks
alias    : sgevcharging
store pw  : ***REDACTED***
key pw    : ***REDACTED***   (PKCS12 forces key pw == store pw)
```

Recommended: enable **Play App Signing** when creating the app (default). Then
Google manages the production signing key and your upload key is the one above.

## Store listing copy

**App name:** SG EV Charging

**Short description (≤80 chars):**
> Find nearby EV charging points in Singapore with live LTA DataMall availability.

**Full description:**
> SG EV Charging helps electric-vehicle drivers find charging points across
> Singapore. Search by postal code or place name, or use your current location to
> rank nearby stations by distance. See live availability (available, occupied,
> unavailable) sourced from LTA DataMall, along with the operator, plug types,
> charging speeds, and how many plugs each location has. Tap "Directions in Maps"
> for turn-by-turn navigation in Google Maps.
>
> Features:
> • Search by Singapore postal code or place name
> • Detect your location and rank charging points by distance
> • Live available / occupied / unavailable connector states
> • Operator, plug type, power rating, and last-updated info
> • Map-first interface with quick station chips
> • One-tap driving directions in Google Maps
>
> Charging data is provided by the Singapore Land Transport Authority (LTA) DataMall.

**Category:** Maps & Navigation  **Contact email:** angch@tertiaryinfotech.com
**Privacy policy:** required — host a short page stating location is used only to
find nearby chargers and is not stored or shared.

## App content (required before release)

- **Data safety:** Location (approximate + precise) — used for *App functionality*,
  not collected/shared/stored off device. No account, no analytics, no ads.
- **Content rating:** complete the IARC questionnaire → rates **Everyone**.
- **Target audience:** 18+ (or per your preference); not designed for children.
- **Ads:** No. **Government app:** No.

## Step-by-step: closed testing

1. Go to <https://play.google.com/console> and **Create app**
   (name *SG EV Charging*, language English, App, Free).
2. Complete **App content**: privacy policy URL, data safety, content rating,
   target audience, ads declaration.
3. **Store listing:** paste the copy above; upload `app-icon-512.png`,
   `feature-graphic-1024x500.png`, and the two phone screenshots.
4. Left nav → **Testing → Closed testing → Create track** (e.g. "Alpha").
5. **Testers:** create an email list and add your testers' Google accounts
   (or use a Google Group). Save.
6. **Create new release** on that track → upload
   `app/build/outputs/bundle/release/app-release.aab`.
   Accept Play App Signing if prompted.
7. Add release notes, **Save → Review release → Start rollout to Closed testing**.
8. Google reviews the build (often hours, up to a few days). Once approved,
   share the **opt-in URL** (Console shows it on the track page) with testers.

## Optional: automate uploads later

Add a Play **service account** JSON (Console → Setup → API access), then either:

- **Fastlane:** `fastlane supply --aab app/build/outputs/bundle/release/app-release.aab --track internal --json_key key.json`
- **Gradle Play Publisher** plugin (`com.github.triplet.play`).

Neither is wired in yet (no service-account key present in this environment).

## Rebuild the bundle

```bash
export JAVA_HOME="/Applications/Android Studio.app/Contents/jbr/Contents/Home"
export ANDROID_HOME="$HOME/Library/Android/sdk"
./gradlew :app:bundleRelease
```
