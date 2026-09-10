# Security policy

## Scope

This repository documents Apple Watch companion sideloading work around iLoader/isideload. Security reports may concern documentation here or the linked implementation branches in `Rzbck/iloader` and `Rzbck/isideload`.

## Reporting a vulnerability

Do **not** publish credentials, certificates, provisioning profiles, Apple account data, pairing records, device identifiers, or other sensitive material in a public issue.

If GitHub private vulnerability reporting is available for this repository, use **Security → Report a vulnerability**. If it is not available, open a minimal public issue stating only that you need a private reporting channel; do not include exploit details or secrets.

For vulnerabilities that clearly belong to upstream iLoader or isideload rather than this integration work, prefer the upstream project's security/reporting process.

## Sensitive material that must never be committed

- Apple ID credentials, session tokens, anisette/session material, or authentication cookies;
- signing certificates, private keys, `.p12`, `.pem`, keychain exports, or passwords;
- provisioning profiles (`*.mobileprovision`);
- pairing records or lockdown/remote-pairing credentials;
- real device UDIDs or other persistent device identifiers;
- unredacted logs containing account, device, certificate, or provisioning data;
- Health, GPS, workout, or other personal application data.

## If a secret is committed

Treat it as exposed even if the commit is later removed. Revoke or rotate the affected credential/material first, then clean repository history if necessary.
