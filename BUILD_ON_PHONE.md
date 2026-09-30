# MyMarket APK — phone-only build

This project includes a GitHub Actions workflow that builds the Android APK in the cloud, so Flutter/Android SDK do not need to be installed on the phone.

## Steps
1. Create/sign in to a GitHub account.
2. Create a new repository, for example `mymarket`.
3. Upload the contents of this project to the repository (the folder containing `mobile`, `server`, `.github`).
4. Open **Actions** → **Build MyMarket APK** → **Run workflow**.
5. Wait for the green check to appear.
6. Open the completed workflow run and download the artifact named **mymarket-release-apk**.
7. Extract the downloaded artifact and install `app-release.apk` on the Android phone.

## Important
- This produces a test/release APK from the current source.
- Payment and OTP are not live until real provider credentials are configured securely on the backend.
- Never put passwords or secret API keys in the repository.
