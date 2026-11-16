# Driver Income Tracker — Android APK project

A fresh Emerald Green + White Android-first driver ledger built with React, TypeScript, Vite and Capacitor. Package ID: `in.driverincometracker.app`.

## Included
- Dashboard, trip history, fuel, map, documents, reports and settings screens.
- Local persistent records using WebView local storage.
- Trip odometer validation, cash/UPI totals, Porter commission estimate and manual commission override.
- Fuel refill records, mileage and fuel price settings.
- **Fuel remaining estimate:** configure tank capacity, starting litres and calibration odometer, or record a full-tank refill with its odometer. The app adds later refills and subtracts estimated consumption using distance ÷ mileage. It shows a low-fuel warning at 5 L or less.
- **Document photo attachments:** camera/gallery image selection, compressed before saving locally (8 MB source-image limit).
- **Reports:** CSV export, Excel-compatible `.xls` export (HTML spreadsheet format), and print-to-PDF through the Android/browser print dialog.
- JSON backup/restore; backup can be shared through the Android share sheet so the user can choose Google Drive.
- English/Tamil labels and light/dark theme.
- Leaflet + OpenStreetMap map tiles, GPS location and nearby fuel-station lookup using the public Overpass API.

## Important limitations
- This is a source project, not a compiled/signed APK. Build it using Android Studio or the included GitHub Actions workflow.
- Fuel remaining is an **estimate**, not a physical tank sensor. Accuracy depends on correct odometer readings, mileage, tank capacity and refill records. A full-tank entry assumes the tank is filled to its configured capacity.
- The Excel export is an Excel-compatible `.xls` HTML spreadsheet, not a native `.xlsx` workbook. PDF export opens the print dialog; choose Save as PDF on Android.
- Backup can be shared manually to Google Drive. **Automatic unattended Google Drive cloud sync is not implemented**; it requires a configured OAuth sign-in flow and Drive API integration. Do not embed client secrets in the APK.
- Document photos are stored in local app storage (WebView localStorage). Protect the device and back up the app data; this starter does not encrypt document photos separately.
- Public OpenStreetMap tiles and Overpass endpoints have usage limits and are not guaranteed uptime. A production deployment should use a compliant hosted provider and follow service policies.
- The app should be tested with sample records before relying on it for business accounting.

## Build a debug APK locally
Requirements: Node.js 20+, Android Studio, Android SDK and Java supported by the installed Gradle version.

1. Extract the ZIP.
2. Run `npm install`.
3. Run `npm run build`.
4. Run `npm run android:add` once to create the Android project.
5. Run `npm run android:sync`.
6. Run `npm run android:open` and wait for Gradle sync.
7. In Android Studio choose **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
8. The debug APK is normally created at `android/app/build/outputs/apk/debug/app-debug.apk`.

For release distribution, configure your own signing key and build a signed APK in Android Studio.

## GitHub Actions build
A workflow in `.github/workflows/android-apk.yml` builds a debug APK when manually started or pushed to `main`, then uploads it as an artifact. It still requires GitHub to install npm dependencies and Android build tools.

## Map notes
No Google Maps API key is used. OpenStreetMap attribution is displayed. GPS needs Android location permission and HTTPS/native app context. Overpass public services can be busy; retry later if fuel station results are unavailable.
