---
title: Google Drive account
description: Point a self-built Opera at your own Google Cloud project for Drive sync.
---

Opera ships with a default Google Cloud project for Drive sync. If you build Opera yourself, you can use your own Google Cloud project instead. This gives you control over the OAuth consent screen and keeps sync traffic on your own quota.

:::note
This only matters if you build Opera from source. The default project works out of the box for installed builds.
:::

## Why change it

- You are self-hosting Opera for a group and want sync under your own Google account instead of the default one.
- You hit Google's OAuth consent limits on the default project.
- You want the consent screen to show your own app name and logo instead of Opera's.

## Create a Google Cloud project

1. Go to [console.cloud.google.com](https://console.cloud.google.com) and create a new project.
2. In **APIs & Services → Library**, enable the **Google Drive API**.
3. In **APIs & Services → OAuth consent screen**, choose **External**, fill in the app name and support email, then add the `drive.file` scope. You can leave testing mode for personal use; publish the app if others will use it.

## Create OAuth client IDs

You need one client per platform:

### Android

1. In **APIs & Services → Credentials**, create an **OAuth client ID** of type **Android**.
2. Enter your signing certificate's SHA-1 fingerprint (`ai.maestro.opera` is the package name).
3. Copy the generated client ID.

### iOS

Create an **OAuth client ID** of type **iOS** with the bundle identifier `ai.maestro.opera`.

### Web

Create an **OAuth client ID** of type **Web application**. Add an authorized redirect URI that matches where you serve Opera, for example `http://localhost:8081/oauth2redirect/google`. For desktop development Opera binds a fixed loopback port, so also add `http://localhost:46357/oauth2redirect/google`.

## Set the client IDs

Opera reads the web client ID and redirect URI from environment variables:

```bash
export EXPO_PUBLIC_GOOGLE_WEB_CLIENT_ID="your-client-id.apps.googleusercontent.com"
export EXPO_PUBLIC_GOOGLE_REDIRECT_URI="http://localhost:8081/oauth2redirect/google"
```

Android and iOS client IDs are compiled in. Edit `src/services/cloud/GoogleDriveProvider.ts` and replace the constants at the top of the file:

```ts
const ANDROID_CLIENT_ID = 'your-android-client-id.apps.googleusercontent.com';
const IOS_CLIENT_ID = 'your-ios-client-id.apps.googleusercontent.com';
```

Then rebuild the app:

```bash
npm run android
```

## Verify

1. Open **Settings → Backup → Google Drive** and sign in.
2. Google shows your consent screen with your app name.
3. After the sign-in completes, the Drive provider appears as connected.

If sign-in fails, check that the redirect URI in your Google Cloud credentials exactly matches what the app generates. On web, the redirect uses the origin you serve the app from, so the URI must match that origin.
