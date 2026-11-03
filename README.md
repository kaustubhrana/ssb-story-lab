# THE SSB STORY LAB — website update

## Files
- `index.html` — updated page based on the currently deployed file supplied on 3 Nov 2026.
- `kaus-uniform-watermark.png` — transparent watermark asset generated from the supplied uniform image.
- `Code.gs` — Apps Script backend update for required/unique email and registration acknowledgement email.

## Important backend setup
1. Open the Apps Script project currently connected to the live Google Sheet.
2. Replace its code with `Code.gs`.
3. Keep this Apps Script bound to the existing master enrolment spreadsheet. The code uses `SpreadsheetApp.getActiveSpreadsheet()` and the tab name `Registrations`; no spreadsheet ID needs to be copied.
4. Confirm row 1 columns A:N match the header order documented at the top of `Code.gs`. Do not add/reorder columns for this version.
5. Save, then Deploy → Manage deployments → Edit the existing Web App deployment → select **New version** → Deploy. Keep **Execute as: Me** and **Who has access: Anyone**. The existing `/exec` URL should remain the same when editing the deployment.
6. Authorise the new email permission if Google prompts. You can run `testRegistrationEmail` once after replacing `YOUR_EMAIL_ADDRESS_HERE` with your own address, then restore the placeholder if desired.
7. Test the endpoint by opening the `/exec` URL; it should return `ONLINE`.

## Website deployment
1. Upload `index.html` and `kaus-uniform-watermark.png` together to the root of the existing GitHub Pages repository.
2. Commit the two files. Do not rename the image asset unless you also update its filename in `index.html`.

## Test checklist
- Submit a new test email: it should appear in column E and receive the acknowledgement email.
- Try the same email again: the page should reject it before creating a second registration.
- Try a blank or malformed email: the inline message should appear and no registration/payment should start.
- Complete a test registration and scan the QR: confirm it shows the correct payee, amount, and registration reference before authorising payment.
- Verify payment independently in the bank/UPI account. The sheet remains `PENDING` until you manually verify payment; this script does not automatically verify UPI transactions.

## Notes
- The QR is generated in the browser using QRCode.js loaded from cdnjs; it contains the dynamic UPI URI for that registration.
- The email availability check is a JSONP read-only check. The backend also checks for duplicate email under a script lock immediately before appending, so the backend remains authoritative.
- The existing frontend uses `fetch(..., mode: "no-cors")` for Apps Script POSTs. The browser cannot inspect the POST response. As before, the page proceeds after the request is sent; the backend is responsible for rejecting any race-condition duplicate.
- Email delivery failure does not delete or cancel a successfully saved registration.
