# Evergreen Online Banking (React)

Evergreen is a simulated online banking project. It uses React, React Router, Supabase Authentication, and Supabase Postgres so the same demo account and requests can be opened in different browsers.

## Run

1. Install Node.js.
2. Open this project folder in Terminal.
3. The supplied project has `.env.local` configured. If it is missing, copy `.env.example` to `.env.local` and enter the Supabase URL and publishable key.
4. Run `npm install`.
5. Run the SQL in `supabase/schema.sql` from the Supabase Dashboard SQL Editor.
6. In Supabase Authentication, enable Email/Password. For this classroom demo, turn off email confirmation so sign-up works immediately.
7. In Supabase Authentication URL Configuration, allow the local Vite URL and the deployed Vercel URL for password reset redirects.
8. Run `npm run dev` and open the local address shown in Terminal.
9. To make a production build, run `npm run build`.

## Admin sign-in

Email: `admin123@gmail.com`  
Password: `admin123`

The first admin sign-in creates the Supabase Auth user using these demo credentials. The Supabase project must have Email/Password enabled and email confirmation disabled for this first classroom sign-in.

Existing browser-only accounts can be moved online on first sign-in: open the updated app in the browser that has the old account and sign in with its existing email/password. The app creates its Supabase login and copies that account's profile and activity. Then sign in with the same credentials in the other browser. The admin should sign in once to initialize the shared admin account.

## Banking features

- User signup/login and Admin login
- User and Admin modules with protected React Router pages
- PIN-protected balance check; new accounts begin at ₹0
- Linked bank account records with masked account numbers
- Transfers with recipient QR scanning where the browser supports it
- Bill payments, transaction history, and downloadable CSV statements
- Loan requests, admin approval, and repayment installments
- Approved loans use 10% simple annual interest for the selected repayment term
- Automatic recurring payments with weekly, monthly, or quarterly schedules, pause/resume controls, and payment history
- Profile updates and customer support cases
- Admin customer search/status filters, loan approval, request filters, recurring payment pause/resume controls, transaction search, and support review

Supabase Auth manages sign-in. Account data is saved in Supabase tables with row-level security. Cloud data is loaded after sign-in, so Chrome and Safari share the same profile, balance, loan requests, and transaction history. The admin can view all account rows; users can access their own account row and a limited account directory.

Linked bank account entries keep the bank name, holder name, IFSC, and last four account digits; they are not verified or connected to external bank services. This is a classroom simulation, not a real banking service. Do not enter real banking credentials or financial information.

Recurring payments are simulated using the Evergreen account balance stored in this browser. Due payments are processed while the app is open and checked again when the app is reopened. The browser app cannot access external bank accounts or run scheduled payments while it is closed; real PhonePe-style bank mandates require bank/UPI authorization and a payment provider integration.

## Deploy on Vercel

1. Push this project folder to GitHub. Keep `.env.local` out of Git; it is ignored by `.gitignore`.
2. In Vercel, choose **Add New → Project** and import the GitHub repository.
3. Set **Root Directory** to `evergreen-online-banking` if the project folder is nested in the repository. If the project files are at the repository root, leave Root Directory unchanged.
4. Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_PUBLISHABLE_KEY` to Vercel's Environment Variables for Production (and Preview if needed).
5. Use the Vite settings: install `npm install`, build `npm run build`, output `dist`.
6. Select **Deploy**. The included `vercel.json` sends app routes back to the React entry page, so BrowserRouter routes can load directly.
