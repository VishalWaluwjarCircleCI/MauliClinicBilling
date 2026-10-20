# Mauli Billing — cloud APK build project

**This is source code, not a compiled APK.** GitHub Actions builds the installable debug APK online without Android Studio.

## Prerequisite: deploy the backend
1. Make a backup of the existing Google spreadsheet.
2. Open spreadsheet `1eL7VjcsPH3yQkttdjBYDrgQ_ea7R_I_zz2FwsVG16S4` → Extensions → Apps Script.
3. Paste `backend/Code.gs` into Code.gs and add `backend/Index.html` as HTML file named Index.
4. Run `setup()` to create separate rent tabs. Existing electricity tabs are not modified.
5. Configure admin username `mauliadmin` and a **private** 12+ character password using `configureAdmin`. Do not send the password in chat or commit it to GitHub. Do not store it in a source file.
6. Deploy → New deployment → Web app, Execute as Me; choose appropriate access for devices and verify your Google account security. Copy HTTPS `/exec` URL.

## Build online (no laptop software installation)
1. Create a **private** GitHub repository and upload the contents of this folder, including `.github/workflows/build-apk.yml` (GitHub web UI supports file upload; keep folder paths).
2. Go to Actions → Build Mauli Billing APK → Run workflow.
3. Paste the deployed Apps Script HTTPS `/exec` URL into `billing_url` and run.
4. Open successful run → Artifacts → download `MauliBilling-debug-apk`, unzip it, and install `app-debug.apk` on Android. Enable install from this source only when you trust your own build.
5. On two devices log in as `mauliadmin`, add a rent payment on one, wait up to 60 seconds or reload the other, and verify in Google Sheet.

## Scope / limitations
- Backend currently supports rent billing, rent payments, charts, and admin login.
- Electricity billing data sync **is not implemented**. `backend/Original_Electricity_App.html` is included only as reference.
- Existing spreadsheet structure has not been independently inspected.
- This is a WebView wrapper. Google Apps Script pages may behave differently inside Android WebView, including authentication redirects. Test login before relying on it.
- The debug APK is not Play Store ready, and reinstalling a future signed release may require migration.
- GitHub builds require account access and Actions availability. A GitHub Actions workflow cannot be run from this chat.
- For sensitive financial data, consider a professionally managed identity/authentication system; this starter password mechanism is not independently security audited.
