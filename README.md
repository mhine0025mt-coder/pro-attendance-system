# ProAttend PRO Final

A responsive Attendance Monitoring / DTE / Payroll-ready web app for GitHub Pages.

## Included modules
- Dashboard
- Employee Management
- Attendance / Daily Time Entry
- Leave Management
- Holiday Management
- Overtime Management
- Payroll
- Payslip Generator
- Reports
- Users / Roles information
- System Settings
- Firebase Email/Password authentication
- Firebase Firestore sync for employees and records
- Mobile and desktop responsive layout
- Print-friendly pages

## Firebase project
This build is configured for the existing ProAttend Firebase web app:
`proattend-3fd57`

Do not share the Firebase account password. The web API key in the client configuration is a public client configuration value.

## Firestore collections used
`employees`, `attendance`, `leaves`, `holidays`, `overtime`

## Important production note
The existing project rules were configured as authenticated-user read/write during development. Before real company payroll use, replace them with role-based Firestore rules and restrict access by user/role.

Payroll in this build is a configurable base calculation:
daily rate when present + approved overtime − optional late deduction.
Company-specific statutory deductions, allowances, holiday/rest-day premiums and night differential should be configured/implemented before production payroll use.

## GitHub Pages
Upload these files to the repository root and commit to `main`:
- index.html
- styles.css
- app.js
- manifest.json
- README.md


## Employee kiosk
The login screen includes **Employee Time In / Out**. An employee enters their Employee ID. The first press records Time In and the second press records Time Out for the current date, with the attendance record written to Firestore.

### Required Firebase setting
Because employees do not need admin passwords, this kiosk uses Firebase Anonymous Authentication. In Firebase Console:
Authentication → Sign-in method → Anonymous → Enable.

Then publish `firestore.rules` in Firestore Rules. Do not use the old wide-open authenticated-only rules for production.

### Security note
Employee-ID-only clocking is convenient but is not strong identity verification: someone who knows another employee's ID could clock for that employee. For production payroll, add a PIN, QR/ID card, device controls, or another identity verification method.
