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

## Repository administration state

Repository setup is complete for the current documentation-only phase.

Verified repository state:

- issues enabled;
- wiki disabled;
- projects disabled;
- squash merge enabled;
- rebase merge enabled;
- merge commits disabled;
- update-branch enabled;
- merged branches deleted automatically;
- topics set to `apple`, `apple-watch`, `iloader`, `ios`, `isideload`, `sideloading`, `watchos`, `windows`;
- MIT license detected by GitHub.

The authenticated owner CLI command also completed successfully for:

- secret scanning;
- secret scanning push protection;
- vulnerability alerts;
- private vulnerability reporting.

The connected GitHub API can verify the public repository/merge/topic state but cannot read back the private-vulnerability-reporting endpoint. Preserve the successful owner-CLI result as configuration evidence unless a later GitHub check contradicts it.

See `docs/REPOSITORY_SETTINGS.md`.

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
- current regression-branch HEAD at this checkpoint: `a38f3942adb89347fa3ba346aa7b0b79b72a3b86`
- all commits after `f7b9f3da...` are documentation-only at this checkpoint
- owns: nested bundle discovery, App ID/profile handling, dependent identifier rewriting, capability-aware provisioning, Watch-target provisioning, nested Watch signing, paired-Watch install backend

### iLoader

- fork: `Rzbck/iloader`
- regression branch: `feat/watch-companion-support-20260909`
- physically validated source anchor: `70f37e9b4afc659ab44ec1944c034093f4cda416`
- CI run for anchor: `34436587217` — SUCCESS
- current regression-branch HEAD at this checkpoint: `fc05ca74e40ec70d33bfa6307c61f7f9e5145a66`
- all commits after `70f37e9b...` are documentation-only at this checkpoint
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

## Current upstream review candidate — isideload

A clean PR candidate has now been prepared separately from the regression branch.

- upstream target repository: `nab138/isideload`
- upstream target branch: `apple-codesign-quick`
- upstream base SHA verified immediately before PR preparation: `2dd6efe864e744aa3aea9d795e2554dc4d8df744`
- fork PR branch: `Rzbck/isideload:pr-watch-companion-support-20260910`
- PR source SHA: `a45cf32614df9a0a26de8c1bb0a5a8c236f2d479`
- commit count above base: 1
- functional diff: 10 files; no HANDOFF, README, workflow, application-specific files, or historical debug documentation
- HealthKit-specific capability workaround intentionally removed from the PR candidate so the upstream review stays scoped to generic Watch companion support
- exact PR-branch build run: `34476518691` — SUCCESS on Ubuntu, Windows, and macOS
- validation-only branch: `validation-watch-companion-tests-20260910`
- validation workflow run: `34476596256` — SUCCESS; `cargo test -p isideload --lib` and build succeeded on Ubuntu, Windows, and macOS
- audit: no Watch Tracker bundle IDs, personal paths, Health/GPS data, UDIDs, credentials, provisioning material, or application-specific artifacts in the PR diff
- upstream history search found no existing PR or commit matching Apple Watch/watchOS/companion support at this checkpoint

Physical validation belongs to the historical regression pair, not to `a45cf326...` itself. The regression pair is a superset that also included HealthKit capability handling. The PR description must preserve that distinction.

An attempt to create the cross-repository Draft PR through the connected GitHub integration returned `403 Resource not accessible by integration`. This is a connector permission limitation on the upstream repository, not a source/CI failure. The repository owner must create the Draft PR through their authenticated GitHub CLI session using the already-prepared branch and description. After creation, record the upstream PR number/URL here and in issue `#1`.

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
- `docs/REPOSITORY_SETTINGS.md`
- `.github/PULL_REQUEST_TEMPLATE.md`
- `.github/ISSUE_TEMPLATE/bug_report.yml`
- `.github/ISSUE_TEMPLATE/validation_report.yml`

## Next exact step

1. Create the Draft PR from `Rzbck:isideload/pr-watch-companion-support-20260910` to `nab138/isideload:apple-codesign-quick` using the authenticated owner GitHub CLI session.
2. Verify the resulting PR is draft, base is `apple-codesign-quick`, head is `Rzbck:pr-watch-companion-support-20260910`, and source SHA is `a45cf326...`.
3. Verify the upstream pull-request CI/checks and inspect the published diff.
4. Record the PR number/URL in this HANDOFF and issue `#1`.
5. Handle maintainer review without merging unless explicitly approved.
6. Keep the HealthKit capability workaround outside this Watch-support PR unless the maintainer explicitly asks for it.
7. Only after the backend review shape is stable, prepare the matching iLoader draft PR.

## Do not do automatically

- do not merge either fork into `main`;
- do not publish a release/crate/installer;
- do not delete, rebase away, squash away, or force-push known-good regression anchors;
- do not copy the Watch Tracker app into this repository;
- do not claim upstream endorsement;
- do not open both upstream PRs at once before the backend shape is understood.
