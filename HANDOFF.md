# HANDOFF — Apple Watch companion support for iLoader

Date: 2026-09-10

## Objective

Maintain a clean public entry point for the physically validated Apple Watch companion sideloading work, while keeping implementation source in the correct iLoader/isideload forks and preparing professional upstream reviews.

## Public repository

- repository: `Rzbck/iloader-watch-companion`
- visibility: public
- default branch: `main`
- language: English
- purpose: architecture, compatibility, validation, security, contribution guidance, and upstream-review coordination
- public tracking issue: `#1` — `Prepare clean upstream Watch companion contribution`
- this repository must not contain Watch Tracker application code or personal test data

## Upstream projects

- official iLoader: `nab138/iloader`
- official isideload: `nab138/isideload`
- iLoader source is MIT licensed, but its name/logos/branding are subject to a separate upstream branding notice
- this repository must always state that it is independent community work and link to the official iLoader project

## Implementation source of truth

### isideload

- fork: `Rzbck/isideload`
- regression branch: `feat/watch-companion-support-20260909`
- physically used source anchor: `f7b9f3da570edd6824c29680545e710846d07df5`
- CI run for anchor: `34436382782` — SUCCESS
- current regression-branch HEAD at this checkpoint: `5fdc15fa10de927b9fcd962eba4f97bb46e3e44e`
- commits after `f7b9f3da...` are documentation-only at this checkpoint
- owns: nested bundle discovery, App ID/profile handling, dependent identifier rewriting, capability-aware provisioning, Watch-target provisioning, nested Watch signing, paired-Watch install backend

### iLoader

- fork: `Rzbck/iloader`
- regression branch: `feat/watch-companion-support-20260909`
- physically validated source anchor: `70f37e9b4afc659ab44ec1944c034093f4cda416`
- CI run for anchor: `34436587217` — SUCCESS
- current regression-branch HEAD at this checkpoint: `cd5d1dc55824d4f6929675b445cc7e533e96d8e5`
- commits after `70f37e9b...` are documentation-only at this checkpoint
- owns: desktop integration, selected usbmux transport preservation, backend pin/integration, companion-device installation path

Always distinguish current branch HEAD from the exact physically validated source anchors above.

## Regression branch vs review branch

The historical feature branches are intentionally preserved as **regression branches**. They contain the development/debug history that led to the working physical result.

They are **not suitable as direct upstream PR heads**:

- iLoader has diverged from its current `main` and contains historical documentation in addition to the small integration changes;
- isideload has diverged from its current `main` and the branch-level diff includes broad dependency/lockfile/auth/certificate/sideloading history in addition to Watch-specific work.

For upstream review, create fresh cleanup/review branches from the relevant current upstream bases and port only the minimum generic Watch-support changes. Never force-push or rewrite the known-good regression anchors to make the PR history prettier.

See `docs/IMPLEMENTATION_MAP.md` for the source-area map and review boundary.

## Physically validated result

The matching iLoader/isideload source anchors were tested through the Windows one-click sideload path on a real iPhone and paired Apple Watch:

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
- `SUPPORT.md`
- `CONTRIBUTING.md`
- `CODE_OF_CONDUCT.md`
- `docs/ARCHITECTURE.md`
- `docs/IMPLEMENTATION_MAP.md`
- `docs/COMPATIBILITY.md`
- `docs/TESTING.md`
- `docs/UPSTREAM.md`
- `.github/PULL_REQUEST_TEMPLATE.md`
- `.github/ISSUE_TEMPLATE/bug_report.yml`
- `.github/ISSUE_TEMPLATE/validation_report.yml`

## Next exact step

Work from public tracking issue `#1` and prepare the **isideload upstream review first**:

1. verify current `nab138/isideload` and `Rzbck/isideload` refs before changing code;
2. read the fork's public-review HANDOFF/porting notes plus `docs/IMPLEMENTATION_MAP.md` here;
3. preserve `f7b9f3da...` as the physical regression anchor;
4. create a new review branch from the relevant current upstream base;
5. port only the Watch-specific behavior needed for the validated path;
6. exclude historical HANDOFF/debug-only files and unrelated dependency/auth/certificate changes unless proven necessary;
7. add/retain focused tests;
8. run exact-SHA tests/CI;
9. inspect the final diff for secrets/private identifiers;
10. open a draft PR to `nab138/isideload`;
11. handle maintainer review without merging unless explicitly approved;
12. only after the backend review shape is stable, prepare the matching iLoader draft PR.

## Do not do automatically

- do not merge either fork into `main`;
- do not publish a release/crate/installer;
- do not delete, rebase away, squash away, or force-push known-good regression anchors;
- do not copy the Watch Tracker app into this repository;
- do not claim upstream endorsement;
- do not open both upstream PRs at once before the backend shape is understood.
