# Indirimbo 500 — Play Store Build Guide

## App Details
- **App ID:** `igitabo.cyindirimboza500`
- **App Name:** Indirimbo 500
- **Version:** 1.0.0

---

## Prerequisites (install once)

1. **Node.js** (v18+) — https://nodejs.org
2. **Android Studio** — https://developer.android.com/studio
3. **Java JDK 17** — comes with Android Studio
4. **Android SDK 34** — install via Android Studio → SDK Manager

---

## Step 1 — Install dependencies

Open a terminal in this folder and run:

```bash
npm install
```

---

## Step 2 — Sync Capacitor

```bash
npx cap sync android
```

This copies `www/index.html` into the Android project.

---

## Step 3 — Create a Signing Keystore (one-time)

```bash
keytool -genkey -v \
  -keystore indirimbo500-release.jks \
  -alias indirimbo500 \
  -keyalg RSA \
  -keysize 2048 \
  -validity 10000
```

⚠️ **IMPORTANT:** Keep this `.jks` file safe — you can NEVER upload updates without it.

---

## Step 4 — Configure signing in build.gradle

Open `android/app/build.gradle` and uncomment the signing block at the bottom.
Fill in your keystore path and passwords.

---

## Step 5 — Build the Release AAB (for Play Store)

```bash
npx cap open android
```

Inside Android Studio:
1. **Build → Generate Signed Bundle / APK**
2. Choose **Android App Bundle (.aab)** ← Play Store prefers this
3. Select your keystore file
4. Choose `release` build variant
5. Click **Finish**

Output: `android/app/release/app-release.aab`

---

## Step 6 — Upload to Google Play Console

1. Go to https://play.google.com/console
2. **Create new app** → fill in details
3. **App content → Content rating** → complete the questionnaire
4. **Production → Create new release**
5. Upload `app-release.aab`
6. Fill in:
   - Release name: `1.0.0`
   - Release notes (see `fastlane/metadata/android/en-US/changelogs/1.txt`)
7. **Review and rollout**

---

## Play Store Listing (copy-paste ready)

### App Title
```
Indirimbo 500
```

### Short Description (max 80 chars)
```
Igitabo cy'indirimbo 500 zo guhimbaza Imana — ari offline, gifite ishakiro.
```

### Full Description
See: `fastlane/metadata/android/en-US/full_description.txt`

### Category
`Music & Audio` or `Books & Reference`

### Content Rating
`Everyone` — no violence, no adult content

### Tags / Keywords
```
indirimbo, kinyarwanda, hymns, guhimbaza imana, rwanda, christian, worship, offline
```

---

## Required Assets for Play Store

| Asset | Size | Notes |
|-------|------|-------|
| App Icon | 512×512 px PNG | Dark red `#1A0004` bg, gold `#d4a23a` music note |
| Feature Graphic | 1024×500 px | Banner shown on Play Store listing |
| Screenshots (phone) | min 2, max 8 | 1080×1920 or similar |
| Screenshots (tablet) | optional | 1200×1920 |

Place screenshots in: `fastlane/metadata/android/en-US/images/phoneScreenshots/`

---

## Project Structure

```
indirimbo500/
├── www/
│   └── index.html          ← Your app (the HTML file)
├── android/
│   ├── app/
│   │   ├── build.gradle    ← App config + signing
│   │   ├── proguard-rules.pro
│   │   └── src/main/
│   │       ├── AndroidManifest.xml
│   │       ├── java/igitabo/cyindirimboza500/
│   │       │   └── MainActivity.java
│   │       └── res/
│   │           ├── values/ (strings, styles, colors)
│   │           ├── mipmap-*/  ← App icons go here
│   │           └── xml/network_security_config.xml
│   ├── build.gradle
│   ├── settings.gradle
│   └── gradle.properties
├── fastlane/metadata/android/en-US/
│   ├── title.txt
│   ├── short_description.txt
│   ├── full_description.txt
│   └── changelogs/1.txt
├── capacitor.config.json   ← Capacitor settings
├── package.json
└── README.md               ← You are here
```

---

## App Icon Sizes Needed

Place PNG files in the correct `mipmap-*` folders:

| Folder | Size |
|--------|------|
| `mipmap-mdpi` | 48×48 |
| `mipmap-hdpi` | 72×72 |
| `mipmap-xhdpi` | 96×96 |
| `mipmap-xxhdpi` | 144×144 |
| `mipmap-xxxhdpi` | 192×192 |

Name them: `ic_launcher.png` and `ic_launcher_round.png`

---

## Support
App Package ID: `igitabo.cyindirimboza500`
Play Store URL: https://play.google.com/store/apps/details?id=igitabo.cyindirimboza500
