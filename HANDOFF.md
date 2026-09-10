# HANDOFF — Apple Watch companion support for iLoader

Date: 2026-09-10

## Objective

Maintain a clean public entry point for the physically validated Apple Watch companion sideloading work, while keeping implementation source in the correct iLoader/isideload forks and preparing professional upstream reviews.

## Public repository

- repository: `Rzbck/iloader-watch-companion`
- visibility: public
- language: English
- purpose: architecture, compatibility, validation, security, contribution guidance, and upstream-review coordination
- this repository must not contain Watch Tracker application code or personal test data

## Upstream projects

- official iLoader: `nab138/iloader`
- official isideload: `nab138/isideload`
- iLoader is MIT licensed, but its name/logos/branding are subject to a separate upstream branding notice
- this repository must always state that it is independent community work and link to the official iLoader project

## Implementation source of truth

### isideload

- fork: `Rzbck/isideload`
- working branch: `feat/watch-companion-support-20260909`
- physically used regression anchor: `f7b9f3da570edd6824c29680545e710846d07df5`
- owns: nested bundle discovery, App ID/profile handling, dependent identifier rewriting, capability-aware provisioning, Watch-target provisioning, nested Watch signing

### iLoader

- fork: `Rzbck/iloader`
- working branch: `feat/watch-companion-support-20260909`
- physically validated regression anchor: `70f37e9b4afc659ab44ec1944c034093f4cda416`
- owns: desktop integration, selected usbmux transport preservation, backend pin/integration, companion-device installation path

Feature branch HEADs may later contain documentation-only commits. Always distinguish current branch HEAD from the exact physically validated source SHAs above.

## Physically validated result

The matching iLoader/isideload revisions were tested through the Windows one-click sideload path on a real iPhone and paired Apple Watch:

- iPhone host installed;
- iPhone host launched;
- embedded Watch companion was discovered/provisioned/signed;
- Watch installation completed rather than remaining a placeholder;
- Watch companion launched.

The tested application also required HealthKit capability provisioning. This confirms that specific tested capability path, not universal entitlement support.

## What is NOT proven

Do not claim universal support for:

- every iOS/watchOS version or Apple device;
- every entitlement/capability;
- every nested Watch/extension topology;
- independent Watch-only apps;
- App Store/TestFlight distribution;
- arbitrary malformed IPA repair.

## Security / privacy rules

Never commit:

- Apple credentials, account/session tokens, anisette material;
- signing certificates/private keys or `.p12`/`.pem` files;
- provisioning profiles;
- pairing records;
- real UDIDs/device identifiers;
- unredacted private installation logs;
- Health, GPS, workout, or other personal application data;
- local application-project paths or application-specific bundle identifiers unless sanitized as examples.

Use generic examples such as `com.example.host` and `com.example.host.watchkitapp`.

## Current public documentation

Read before changing the project:

- `README.md`
- `NOTICE.md`
- `SECURITY.md`
- `CONTRIBUTING.md`
- `CODE_OF_CONDUCT.md`
- `docs/ARCHITECTURE.md`
- `docs/COMPATIBILITY.md`
- `docs/TESTING.md`
- `docs/UPSTREAM.md`

## Next exact step

Prepare the **isideload upstream review first**:

1. verify the current `Rzbck/isideload` branch HEAD and git diff against the relevant upstream base;
2. read its current public-review HANDOFF/porting notes;
3. preserve `f7b9f3da...` as the hardware regression anchor;
4. create a separate cleanup/review branch if needed rather than rewriting the known-good branch;
5. remove historical diagnostics and application-specific assumptions from the proposed patch;
6. run tests/CI on the exact review SHA;
7. inspect the final diff for secrets/private identifiers;
8. open a draft PR to `nab138/isideload`;
9. handle maintainer review without merging unless explicitly approved;
10. only then prepare the matching iLoader draft PR.

## Do not do automatically

- do not merge either fork into `main`;
- do not publish a release/crate/installer;
- do not delete or rewrite known-good regression branches/SHAs;
- do not copy the Watch Tracker app into this repository;
- do not claim upstream endorsement;
- do not open both upstream PRs at once before the backend shape is understood.
