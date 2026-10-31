
# Daily Travel - BOOK • RIDE • EXPLORE - GitHub + Supabase Live Version

Your apps are 100% same look & working, now with real MTN MoMo & Airtel Money split.

## Live Supabase Already Injected
URL: https://qjffybockawpfpvanpzw.supabase.co
Anon Key: eyJhbGciOiJIUzI1NiIs...

Files already contain your credentials - just push to GitHub!

## Structure
- `index.html` -> Customer + Company app (main) - this is what GitHub Pages serves as home
- `client.html` -> same as index (backup)
- `admin.html` -> Admin monitoring + adjustable registration fee + commission
- `supabase.sql` -> RUN THIS FIRST in Supabase SQL Editor
- `supabase/functions/` -> Real payment backend (MTN + Airtel)
- `assets/logo.jpg` -> Your logo

## How Payments Work (Real Time, Hidden Breakdown)

**Customer sees ONLY final price:** e.g., UGX 32,040

**Behind scenes:**
```
Base fare 30,000 -> Company MTN/Airtel code (direct)
Commission 1,500 (5%) -> Admin MTN/Airtel code (direct)
Provider fee 540 (1.8%) -> MTN/Airtel charges
Total 32,040 -> Customer pays
```

Code in `disburse-payment` does the split automatically.

## Setup Steps to Go Live in 5 Minutes

### 1. Supabase SQL
Supabase Dashboard -> SQL Editor -> Paste & Run `supabase.sql`
Then Table Editor -> `platform_settings` (id=1) -> Set:
- `registration_fee`: 50000
- `commission_percent`: 5
- `admin_mtn_code`: YOUR MTN MoMo number (e.g., 256771234567)
- `admin_airtel_code`: YOUR Airtel merchant code
- `mtn_fee_percent`: 1.5
- `airtel_fee_percent`: 1.5

### 2. GitHub Pages
- Create repo `daily-travel`
- Upload ALL files in this zip to repo root
- Settings -> Pages -> Source: Deploy from branch -> main -> / (root) -> Save
- Your live link: `https://YOURUSERNAME.github.io/daily-travel/`
- Admin link: `https://YOURUSERNAME.github.io/daily-travel/admin.html`

Open on 2 devices = same data (Supabase Realtime).

### 3. Edge Functions (For Real Money - Optional for Testing)

Without keys, payments run in **SIMULATION MODE** - everything works, but no real money moves (logs show [SIM]).

To go REAL:

**Supabase CLI:**
```bash
npm install -g supabase
supabase login
supabase link --project-ref qjffybockawpfpvanpzw
```

**Set Secrets (Supabase Dashboard -> Edge Functions -> Secrets):**
```
MTN_COLLECTION_SUBSCRIPTION_KEY=your_mtn_collection_sub_key
MTN_COLLECTION_API_USER=your_api_user
MTN_COLLECTION_API_KEY=your_api_key
MTN_DISBURSEMENT_SUBSCRIPTION_KEY=your_disbursement_sub_key
MTN_DISBURSEMENT_API_USER=...
MTN_DISBURSEMENT_API_KEY=...
MTN_TARGET_ENV=mtnuganda (or sandbox for testing)

AIRTEL_CLIENT_ID=...
AIRTEL_CLIENT_SECRET=...
AIRTEL_PIN=...
AIRTEL_ENV=production (or sandbox)
```

**Deploy:**
```bash
supabase functions deploy disburse-payment
supabase functions deploy momo-collect
supabase functions deploy momo-disburse
supabase functions deploy airtel-collect
supabase functions deploy airtel-disburse
```

### 4. Test

- Register a bus company -> Pay registration fee (goes to your Admin MoMo)
- Admin approves -> Company appears in Client app instantly
- Company adds bus/route/schedule
- Company -> Seat Manager -> Block 2 seats as offline sold
- Customer on another phone -> Those seats show black/taken, can't buy
- Customer buys ticket -> Money splits to company + admin instantly

## Logo
Original logo preserved. File in `assets/logo.jpg` - apps use data URI so it works offline too.

## Support
All apps linked via Supabase Realtime. No localStorage limit anymore.

BOOK • RIDE • EXPLORE
