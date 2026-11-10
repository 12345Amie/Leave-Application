# SEDC Energy - Leave Application (Firebase + Vercel)

Files: `index.html` (the app), `firebase-config.js` (your Firebase settings), `firestore.rules` (security rules).

## Part 1 - Firebase (about 10 minutes)
1. Go to https://console.firebase.google.com > **Add project** (any name, e.g. sedc-leave). Google Analytics can be off.
2. **Build > Authentication > Get started > Email/Password > Enable > Save.**
3. **Build > Firestore Database > Create database.** Choose *Production mode* and a nearby region (e.g. asia-southeast1 Singapore).
4. Firestore > **Rules** tab: delete everything, paste the contents of `firestore.rules`, click **Publish**.
5. **Project settings (gear icon) > General > Your apps > Web (</>)**. Register an app, copy the `firebaseConfig` values, and paste them into `firebase-config.js`.

## Part 2 - Vercel
1. Put these 4 files in a GitHub repository (index.html, firebase-config.js, firestore.rules, README.md).
2. Vercel > **Add New > Project** > import that repository. Framework Preset: **Other**. No build command. Click **Deploy**.
   (Alternative without GitHub: install Node, open a terminal in this folder, run `npx vercel --prod`.)
3. Copy your site address (for example `sedc-leave.vercel.app`).
4. Back in Firebase: **Authentication > Settings > Authorized domains > Add domain** and add that address. Sign-in will not work until you do this.

## Part 3 - First use
1. Open your site, choose **Create account**, and register with **Hr@sedcenergy.com**. Open the verification email and click the link, then sign in.
2. HR sees extra tabs: **HR records, Reports, Approved staff**. In *Approved staff*, paste your staff emails and click Add.
3. Tell staff to open the site, create an account with their approved email, verify it, and sign in.

## Notes
- To add another HR person, add their lowercase email in two places: `HR_EMAILS` in `index.html` and the `isHR()` line in `firestore.rules` (then re-publish the rules and redeploy).
- Staff can only see their own applications. HR can see everyone's and change the status. Nobody can delete records.
- Firebase config values are not secret; the security rules protect the data.
- Supporting documents (MC) are not uploaded; staff attach them to the email to HR. Uploading files would need Firebase Storage later.
- Export CSV in HR records is your backup copy.
