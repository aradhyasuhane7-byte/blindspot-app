# Direct department login

Open **Login → Prepared user IDs & passwords — all 5 departments**. Enter your private access code (provided separately in ChatGPT), then select **Use login** for your department and press **Login**. No business-owner sign-in is needed. IDs: `bs.admin`, `bs.confirm`, `bs.pack`, `bs.doc`, `bs.del`. Save your private login sheet from that panel. Never publish it or the access code.

The source ZIP contains salted password hashes, not plaintext credentials. The password panel requires the hosted secret `BLINDSPOT_PREPARED_LOGIN_CONFIG`, which is installed on your live website and excluded from this download. A separate local copy needs its own credentials/runtime configuration. If an account password is changed later, the panel stops showing the old password.

# Business access

Use **Login → Business owner sign-in** for the initial setup. Create your workspace, set your admin login in Operations tools → Settings & profile, and add employee accounts in Employees & access. Previous public testing accounts are disabled. Your queue starts empty; add or import your real orders.

# Blindspot user guide

## Public visitors

The main page is read-only. Anyone can see only the order fields a business admin has published. Customer contacts, financial values, employee identities, notes and proof photos remain behind login. Use search and the page controls to find records.

## Employees

Choose your department at Login and use your assigned ID/password. Check that the header shows your correct account and department. Your account can complete only its assigned workflow stage. Opening another stage or scanning a label never grants permission to update it.

- Confirmation verifies and accepts the order.
- Packaging prepares and packs it.
- Documentation & Dispatch saves courier/tracking details and confirms handover.
- Delivery records delivery completion.

Use **My assignments** to focus on orders assigned to you. Open an order to record a delay reason, add a note or optional photo proof, and complete your stage. Overdue orders are escalated in-app to assigned staff, relevant department leads and head admin. An acknowledgement records the action being taken; it does not erase a delay. Email/SMS escalation is not active.

## Head admin

The admin can create/edit orders, process every stage, assign employees per stage and designate department leads in **Employees & access**. Regular department staff retain their own-stage permissions. Manual completion overrides require a reason and are reversible. Archive is reversible too.

## Password recovery

Use **Forgot password / recover account** on Login. Either verify the exact registered email with ChatGPT, or request recovery from your business admin.

Admins open **Safety & recovery → Password recovery** and issue a reset link for the verified employee. Links expire after 20 minutes and work once. Share the link directly with the employee; the application does not automatically email it. After resetting, all old app sessions are revoked.

## QR and barcode scanning

Click **Scan QR / barcode**. You can use your device camera, choose a clear label image, scan with a USB scanner into the input, or type the order/tracking number. QR labels can be downloaded from the order desk. Scanning opens a record and leaves its stage unchanged until an authorized employee explicitly completes it. Camera access depends on browser/device permission and HTTPS.

## Privacy

Open **Safety & recovery → Public privacy**. Toggle publication and choose exactly which of the six supported order fields may appear publicly. Disabled fields are omitted by the backend. Preview your workspace through its read-only link.

## Reporting

The queue has 25 rows per page. The application syncs database pages before updating its complete analytics dataset. CSV, Excel-compatible XML, Tally mapping CSV and JSON downloads read the full database rather than stopping at the old 2,000-order cap. Very large datasets can take longer to sync or download. Weekly/monthly exports filter by received time in IST. Tally mapping still requires an accountant's ledger/voucher mapping.

## Backups and recovery

Open **Safety & recovery → Backups & restore**.

- Successful data changes produce private cloud recovery records.
- Full checksummed snapshots are created on activity each day, before major operations and on demand.
- Backups are write-triggered; there is no independent closed-site daily timer.
- A failed automatic backup is reported without pretending the already-committed database save failed.
- Preview recovery verifies snapshot parts and shows record counts.
- For latest recovery, replay later saved changes. For a historical recovery, turn that option off.
- Type RESTORE before applying recovery. A rollback snapshot is saved first.

Recovery restores matching/additional order records and settings, preserves newer records/current audit history, and does not restore employee access or passwords. Private photo objects remain in cloud storage; recovery files contain their references, not duplicate image bytes. Backup files are not automatically deleted by a retention policy.

## Error monitoring

Open **Safety & recovery → Error monitoring** for recorded browser, save and backup failures. Review the error, address its cause and mark it reviewed. The safety tab shows an issue count. Error messages redact credential-like values and email addresses. Monitoring is in-app; no external incident email is configured.

## Customer care and assistant

Use Customer care for email contact, the published phone number, support requests and instant product FAQ answers. Contact email: aradhyasuhane7@gmail.com. Phone: +91 7509595171.

Support tickets are saved in the owner-only inbox; email links open drafts. Human response times are separate from automated help. Live generative AI is configured but requires OpenAI API billing activation. Automatic hourly email summaries are not activated. The FAQ assistant cannot access private orders or change records.

## Prepare all five logins

After Business owner sign-in and workspace setup, open **Employees & access → Create all 5 logins**. This creates any missing head admin, Confirmation, Packaging, Documentation & Dispatch, and Delivery accounts with unique IDs and random passwords. Save the private login sheet before closing it. Existing accounts and passwords remain unchanged; use account recovery for forgotten passwords. Each department can update only its stage. You can also add named employees with real email addresses below. The generated department slots use internal identifiers, so their forgotten passwords require admin-issued recovery links. Passwords are hashed in the database and never included in source downloads.

## AI chat & support

Open the separate **AI Chat** button on any page for the assistant. **Customer Care** has its own button for email, phone and support requests. The assistant answers Blindspot questions about logins, department permissions, order stages, delays, reports and recovery. It cannot look up or modify private orders. User messages/history are sent to OpenAI for AI replies and saved in the customer-care inbox. Avoid sharing credentials or sensitive customer details.

The hosted AI connection is configured securely. At setup, OpenAI returned `billing_not_active`: activate billing in the OpenAI Platform account before live AI replies can work. Saved Blindspot guidance remains available and is identified as such whenever AI is unavailable. The configured starter model is `gpt-6-luna`; API usage is billed separately from ChatGPT subscriptions.

A separate local copy can use `OPENAI_API_KEY` in its ignored `.env.local`. Hosted deployments may use the secret pair `OPENAI_KEY_CIPHERTEXT` / `OPENAI_KEY_JWK` or a direct secret `OPENAI_API_KEY`. Credentials are never included in the source ZIP.

## Delay insights and notifications

Admins see Delay insights on their dashboard: this week to date versus the same elapsed part of last week, using Monday boundaries in IST. The stage ranking uses average recorded late minutes per completion; counts, totals and recurring reasons include order references. Archived records are included; manual override stages are excluded. No-data periods are labelled rather than given a percentage. These statistics describe recorded delays, not proven causes.

Every department has a Notifications panel for orders arriving at its stage and overdue stages. Admin sees the complete workflow. Read status is saved centrally for each account/role and workspace. The centre refreshes every 15 seconds and supports older pages and marking up to 50 displayed items read. It derives handoffs from durable stage completion records and includes existing order history. Archived orders leave the feed. Email and WhatsApp notifications are not sent. Opt-in browser push is available for handoffs.

## Browser handoff notifications

On each employee device: sign in to the correct department, open **Notifications**, click **Enable browser notifications**, and approve the browser prompt. Then click **Send test notification** and confirm the device shows it. When a stage is successfully completed, the server sends an encrypted, generic alert to registered devices for the next department. The site tab can be closed; no page polling or OpenAI billing is needed. Delivery completion alerts go to registered admins. Imports, manual overrides and historic stage records do not send new background alerts.

Push uses browser push services and a service worker. Provider acceptance is not proof that a device displayed the message. Browser/OS restrictions, force-closing the browser, battery settings or network loss can delay/block delivery. Messages expire after 24 hours. On iPhone/iPad, add the site to Home Screen and enable notifications from that installed web app. Permission and closed-tab delivery must be verified on actual employee devices; those prompts were not accepted on the user's behalf during development.

Use **Disable on this device** to opt out. Signing out or changing accounts unsubscribes this browser; re-enable after signing back in. Role changes and revoked memberships are checked server-side before sending. Alerts omit buyer details and order numbers; opening one still requires the appropriate account to view private orders. Delivery failures appear in Error monitoring. There is no guaranteed-delivery or scheduled retry service.

Production VAPID keys are configured in runtime settings (`VAPID_PUBLIC_KEY` / secret `VAPID_PRIVATE_KEY`). Secrets and subscription records are not included in source downloads.
