# helm-data

Data feed for the [Helm dashboard](https://jaderiley.co.za). **Not** application code.

- `snapshot.json` — the dashboard stats, **AES-256-GCM encrypted** (PBKDF2 key from the Helm passcode). Ciphertext only; useless without the passcode, which is why this repo is safe to keep public.
- `status.json` — `{ tunnelUrl, updatedAt }` for the "PC is on — open TRUE LIVE" banner. Plaintext, but the tunnel it points at is itself passcode-gated.

Both files are **force-pushed every 5 minutes** by `publish-github.js` (run by the `ClaudeHelmPublish` scheduled task). History is intentionally kept at a single commit — this is a data feed, not a log. The deployed shell reads them from `raw.githubusercontent.com/jaderiley/helm-data/main/*`.

Replaces the former Vercel Blob store `helm-data`, which was suspended 2026-07-06 for exceeding the free-tier write quota. GitHub raw has no write quota, so that failure mode is gone.
