# Coldesina CRM Gmail Extension — Hosting

Public hosting for the Coldesina CRM for Gmail Chrome extension binary and update manifest. Used by Google Workspace Admin Console to force-install the extension on managed Chrome browsers across coldesinacapital.com.

**This repo is intentionally public** — it only contains the compiled extension `.crx` (which is downloaded and installed on every user's machine anyway) and the `update.xml` manifest pointing Chrome at the latest release. No source code, no secrets.

## Source

The extension source code lives in the private `coldesina-apps` repo, under `gmail-extension/`. This repo is the published-binary mirror.

## Update flow (when releasing a new version)

1. In `coldesina-apps/gmail-extension/`, bump `manifest.json` `"version"` (e.g. `1.0.3` → `1.0.4`).
2. Commit and push source changes to `coldesina-apps`.
3. In Chrome → `chrome://extensions/` → **Pack extension** → use the existing `.pem` (stored in Tony's password manager) so the extension ID stays the same. This produces a new `.crx`.
4. In this repo, edit `update.xml`: bump the `version=` attribute and the `codebase=` URL (point at the new release tag).
5. Commit and push `update.xml` to `main`.
6. Create a new GitHub Release here, tag e.g. `v1.0.4`, attach the new `.crx`.
7. Chrome auto-updates managed installs within ~6 hours of the release going live (or run `chrome://policy/` → Reload policies for instant pickup).

## URLs (used by Workspace Admin Console)

- Update manifest: `https://raw.githubusercontent.com/tcoldesina-cell/coldesina-crm-extension-host/main/update.xml`

## Extension ID

`kcdmiepalmmfhginmjonfjbbffahkcbm` — derived from the `.pem` private key. Reusing the same `.pem` for every release keeps this ID stable. Losing the `.pem` means starting over with a new ID and forcing every user to reinstall.
