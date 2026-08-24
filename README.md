# ටියුෂන් ටීචර් — Production Offline App

Mobile-first tuition/student management app with Sinhala UI.

## Included
- Student add/edit/delete, call and WhatsApp
- Grade 1–5 WhatsApp group links saved centrally
- Group links reused by assignments, extra classes and WhatsApp page
- Monthly fees with payment dates, arrears and future-month payments
- 4-day overdue highlighting and WhatsApp reminder
- Grade-wise ranking and progress charts
- Student progress WhatsApp reports with subject marks and percentages
- Local AI Agent for diagnostics and simple app-data questions
- Backup / Import / full Data Reset / Demo Reset
- Offline PWA service worker

## Run
Open `index.html` in a browser or deploy the folder to a static host such as Netlify.

## Data
Data is stored in browser LocalStorage. Use **දත්ත / සැකසුම් → Backup** before resetting or clearing browser storage.

## Google Drive Auto Backup
The **දත්ත / සැකසුම්** page now has a "Google Drive Auto Backup" card. Whenever data changes (a student added, a fee paid, a score entered, etc.), the app waits a few seconds and then silently uploads a fresh `tuition-teacher-backup.json` to the connected Google Drive account (creating it the first time, updating the same file after that).

This needs a one-time setup that only the app owner can do (Google requires every app to register its own credentials — this can't be pre-filled for you):

1. Go to the [Google Cloud Console](https://console.cloud.google.com/) → create a project (or use an existing one).
2. **APIs & Services → Library** → enable the **Google Drive API**.
3. **APIs & Services → OAuth consent screen** → set it up (External is fine); add your own Google account under **Test users** while the app is unverified.
4. **APIs & Services → Credentials → Create Credentials → OAuth client ID** → Application type **Web application**.
5. Under **Authorized JavaScript origins**, add the exact URL you host this app on (e.g. `https://yoursite.netlify.app`). `file://` origins will not work — the app must be served over `http(s)`.
6. Copy the generated **Client ID** (ends with `.apps.googleusercontent.com`).
7. In the app: **දත්ත / සැකසුම්** → paste the Client ID → **Connect Google Drive** → sign in and approve access → toggle **ස්වයංක්‍රීය Backup** on.

Notes:
- The app only requests the `drive.file` scope, so it can only see/write the one backup file it creates — not your whole Drive.
- Because the OAuth consent screen is unverified by default, only the test users you add in step 3 can connect (fine for a single-teacher app).
- You can trigger an immediate upload any time with **දැන් Backup කරන්න**, and disconnect with **විසන්ධි කරන්න**.
