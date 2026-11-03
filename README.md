# THE SSB STORY LAB — GitHub Pages site

## Files
- `index.html` — mobile-first programme catalogue and enrolment page.

## Before publishing
1. Open `index.html` in a text editor.
2. Find `const UPI_ID = "YOUR_UPI_ID_HERE";`
3. Replace the placeholder with your actual UPI ID (example format: `name@bank`).
4. Check `PAYEE_NAME` and change it to the exact payee name shown in your UPI app.
5. Save the file.

The current prices match the poster:
- PPDT: ₹199 / ₹499 / ₹999
- TAT: ₹499 / ₹1,099 / ₹2,199
- PPDT + TAT: ₹699 / ₹2,199 / ₹2,999

## Publish with GitHub Pages
1. Sign in to GitHub and create a new repository, for example `ssb-story-lab`.
2. Choose **Public** (simplest for GitHub Pages on a free personal account).
3. Add/upload `index.html` to the repository root (not inside another folder).
4. Open the repository's **Settings** → **Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Select branch **main** and folder **/(root)**, then click **Save**.
7. Wait for the Pages deployment to finish. The URL will usually look like:
   `https://YOUR-USERNAME.github.io/ssb-story-lab/`
8. Open that URL on your phone and test all programme/service combinations.
9. Generate the QR code only after the final URL is live. Test the printed/displayed QR from another phone.

## Important payment limitation
This first version creates a UPI payment intent (`upi://pay`) with the selected amount prefilled. It does **not** verify payment, issue receipts, store enrolments in a secure database, or notify you automatically. Confirm every payment independently in your UPI app/bank account before marking a candidate as enrolled. Do not rely on a screenshot or the browser returning to the page as proof of payment.

The form currently validates and uses the entered details in the browser but does not send them to you. Until a backend or form service is connected, ask candidates to message you their reference and details after payment, or add a separate registration form link.

For Razorpay later, use a backend/serverless function to create orders and verify signatures/webhooks. Never put Razorpay secret keys in this public HTML file.

## Updating the page
Edit `index.html`, commit the changes to the `main` branch, and GitHub Pages will redeploy the site.
