# Kestrel threat list (preview)

This repository holds the signed threat list that preview builds of the Kestrel mobile security app
download. It is produced automatically; nothing here is edited by hand.

| File | Content |
|------|---------|
| `list.json` | The signed list: `{"payload": base64, "key_id": "...", "sig": base64}`. The payload is JSON with a version, creation and expiry times and the blocked domain names. The signature is Ed25519 over `"KALKAN-LIST-v1\n" + SHA-256(payload)`. |
| `status.json` | Version, creation and expiry times (Unix seconds), signing key id, number of domains, SHA-256 of `list.json`, and the number of entries each source contributed. |
| `history.jsonl` | The `status.json` of recent publications, one per line. |

The branch is rewritten on every publication (a single commit), so older lists are not kept here.

## Status: preview

The list is signed with a **preview** key. Only debug and preview builds of the app accept it;
release builds do not. Do not rely on this repository for production use: the key, the format and
the location can change without notice.

## Sources

| Source | What it contributes | Terms |
|--------|---------------------|-------|
| CERT Polska warning list (`hole.cert.pl`) | Domain names used for phishing, mostly targeting users in Poland | https://cert.pl/en/warning-list/ |

Entries are normalised, de-duplicated and filtered before signing (well-known legitimate domains and
shared hosting platforms are never listed as a whole).

Naming a source states where the data came from. It does **not** mean that the source cooperates
with, endorses or is otherwise associated with Kestrel. The data is provided without any warranty
of accuracy or completeness, by the sources and by us.

## Reporting a wrong entry

If a domain is listed here by mistake, please report it to the source that listed it (see the table
above) and open an issue in this repository so we can check our filtering.
