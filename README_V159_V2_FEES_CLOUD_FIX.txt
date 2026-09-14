NIKHAT MIDDLE SCHOOL DIGORA
V159 V2 — FEES CLOUD FIX

BASE:
- V159 V2 tested build.
- Student Ledger code is preserved/frozen.

FEE CLOUD ARCHITECTURE:
- Supabase relational fee tables are used:
  fee_opening_balances
  fee_transactions
  fee_allocations
  fee_voids
  audit_logs
- Fee payments are posted through the existing atomic/idempotent
  post_fee_transaction RPC.
- Receipt deletion uses void_fee_transaction; posted transactions are
  not physically deleted.
- Current fee and previous opening due are synchronized through
  fee_opening_balances.
- Paid amounts are derived from fee_transactions + fee_allocations.
- The old nms_fees JSON blob is excluded from the generic school_kv
  sync so it cannot overwrite the relational fee state.
- Local fee UI remains in place and is rebuilt from the cloud relational
  state after synchronization.
- Offline local changes are retained and pushed when cloud is available.
- Fee synchronization is scheduled after local changes and every 3 seconds
  while the app is visible.
- Student records needed by the fee tables are ensured in public.students
  using admission number as the school-level identity.

IMPORTANT:
- Do NOT run the Supabase schema again.
- Do NOT delete any Supabase tables or old projects.
- Use the existing Supabase project and authenticated Admin account.
- This package is a test candidate. Static JavaScript checks passed.
- Live two-device Supabase behavior must still be tested in the real browser.

LOCAL TEST ORDER:
1. Start the app normally.
2. Login with the existing local admin credentials if prompted.
3. Configure/login to the existing Supabase project if the cloud panel
   is not already configured.
4. In Fees, set one student's Previous Due and Current Fee.
5. Collect a small test payment.
6. Confirm Previous Paid, Current Paid, Total Due, Receipt Ledger and
   Student Ledger.
7. Open the same school on the second device and wait a few seconds.
8. Confirm the same values and receipt appear there.
9. Test a second payment from the second device.
10. Confirm it appears back on the first device without manual download.

BUILD:
V159 V2 FEES CLOUD FIX
