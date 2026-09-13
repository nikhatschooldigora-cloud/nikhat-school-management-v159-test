# Nikhat School ERP — Final Clean Build

School: Nikhat Middle School Digora
DISE Code: 23080208912
Address: Near of Jain Mandir, Ward No. 04, Digoar, Tikamgarh, Madhya Pradesh

This build is a clean-from-scratch ERP foundation and does not contain the legacy V159 shared `nms_fees` JSON sync engine.

## Included
- Role-based ERP navigation
- Student/Parent restricted portal
- Students, staff, classes, attendance, fees, exams/marks, report cards, certificates, ID cards, timetable, homework, communication, parent contacts, reports, promotion, users, backup, health and settings
- Offline local data store
- CSV import/export for students and export for staff/attendance/fees
- Transaction-based fee collection with receipt numbers and VOID/audit correction
- PWA files and school logo
- Normalized Supabase schema in `supabase-schema.sql`

## Initial local logins
admin / 1234
principal / 1234
accountant / 1234
office / 1234
teacher / 1234
student / 1234

## Cloud deployment prerequisite
The application cannot safely invent or embed a Supabase project's URL/key. On the administrator device, open Central Database and enter the school's own Supabase project URL and publishable/anon key, then apply `supabase-schema.sql` in the Supabase SQL editor and add production RLS policies. End users do not need a separate Supabase login.

Before production, verify cloud auth/RLS and run multi-device tests. The client deliberately does not perform destructive automatic cloud writes when cloud setup is incomplete.
