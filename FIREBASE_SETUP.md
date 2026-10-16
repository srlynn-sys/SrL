# SrL Firebase Results Setup

The website code and Admin Panel are in place. Complete these Firebase Console steps before testing:

1. Open Firebase Console for project `tamar-lann`.
2. In **Authentication → Sign-in method**, enable **Email/Password**.
3. In **Authentication → Users**, create the teacher account and set a strong password.
4. Copy the teacher account's exact email address.
5. Replace `replace-with-your-teacher-email@example.com` in both `admin.html` and `firestore.rules` with that email. Commit the changes.
6. In **Firestore Database → Rules**, publish the contents of `firestore.rules`. Alternatively, from a trusted computer with Firebase CLI configured for this project, run `firebase deploy --only firestore:rules`.
7. Wait for GitHub Pages to publish, then open `https://srlynn-sys.github.io/SrL/admin.html` and log in with the teacher account.
8. Test by submitting one sample quiz, confirming the score appears in Public score lookup and Admin Panel, then test Reset Individual and Reset All.

## Important limitations of a static public website

- Public score lookup means the Firestore results collection is readable by anyone who can access the project endpoint; a user may be able to enumerate results. Do not store sensitive student information here.
- Scores are calculated in the browser, so a technically skilled user could forge a submission. A server-side trusted scoring endpoint would be needed to prevent this fully.
- The rules permit public result submissions because the static quiz submits from an unauthenticated browser. Admin-only delete/update is protected by the teacher email allowlist.
- Do not replace the rules with unrestricted public write access. If rules are not published, saving and reset functions will fail.
