# HANDOFF — Apple Watch companion support for iLoader

Date: 2026-09-10

## Objective

Maintain a clean public coordination point for the physically validated Apple Watch companion sideloading work, keep implementation source in the correct iLoader/isideload forks, and track upstream review without mixing application-specific data or historical debug material into contribution branches.

## Public repository

- repository: `Rzbck/iloader-watch-companion`
- visibility: public
- default branch: `main`
- language: English
- purpose: architecture, compatibility, validation, security, contribution guidance, and upstream-review coordination
- public tracking issue: `#1` — `Prepare clean upstream Watch companion contribution`
- do not place Watch Tracker application code or personal test data here

## Repository administration state

Verified current repository setup:

- issues enabled;
- wiki disabled;
- projects disabled;
- squash merge enabled;
- rebase merge enabled;
- merge commits disabled;
- update-branch enabled;
- merged branches deleted automatically;
- topics: `apple`, `apple-watch`, `iloader`, `ios`, `isideload`, `sideloading`, `watchos`, `windows`;
- MIT license detected by GitHub.

The authenticated owner CLI also completed successfully for secret scanning, secret-scanning push protection, vulnerability alerts, and private vulnerability reporting. Preserve that owner-CLI result as configuration evidence unless a later GitHub check contradicts it.

## Upstream projects

- official iLoader: `nab138/iloader`
- official isideload: `nab138/isideload`
- iLoader source is MIT licensed, with separate upstream branding restrictions for the iLoader name/logos/assets
- always present this project as independent community work and link to the official upstream projects

## Regression anchors — preserve

### isideload

- fork: `Rzbck/isideload`
- regression branch: `feat/watch-companion-support-20260909`
- physically used source anchor: `f7b9f3da570edd6824c29680545e710846d07df5`
- anchor CI run: `34436382782` — SUCCESS
- regression branch HEAD at this checkpoint: `a38f3942adb89347fa3ba346aa7b0b79b72a3b86`
- commits after `f7b9f3da...` are documentation-only at this checkpoint

### iLoader

- fork: `Rzbck/iloader`
- regression branch: `feat/watch-companion-support-20260909`
- physically validated source anchor: `70f37e9b4afc659ab44ec1944c034093f4cda416`
- anchor CI run: `34436587217` — SUCCESS
- regression branch HEAD at this checkpoint: `fc05ca74e40ec70d33bfa6307c61f7f9e5145a66`
- commits after `70f37e9b...` are documentation-only at this checkpoint

Never rewrite, rebase away, force-push, squash away, or delete these known-good regression anchors merely to improve review history.

## Physically validated result

The matching historical iLoader/isideload source anchors were tested through the Windows sideload path on a real iPhone and paired Apple Watch:

- iPhone host installed;
- iPhone host launched;
- embedded Watch companion was discovered, provisioned, and signed;
- Watch installation completed instead of remaining a placeholder;
- Watch companion launched on physical hardware.

The tested application also required HealthKit capability provisioning. That proves the specific tested capability path only; it is not proof of universal entitlement support.

## Current upstream PR — isideload

Upstream review is now live:

- PR: `nab138/isideload#12`
- URL: `https://github.com/nab138/isideload/pull/12`
- title: `Add Apple Watch companion app sideloading support`
- state: OPEN
- review state: Ready for review (`draft: false`)
- mergeability reported by GitHub at this checkpoint: mergeable
- upstream target branch: `apple-codesign-quick`
- upstream base SHA: `2dd6efe864e744aa3aea9d795e2554dc4d8df744`
- fork head branch: `Rzbck/isideload:pr-watch-companion-support-20260910`
- PR source SHA: `a45cf32614df9a0a26de8c1bb0a5a8c236f2d479`
- commit count above base: 1
- changed files: 10

The PR description is complete and explicitly separates current CI/test evidence from historical physical-device evidence.

### Review-branch validation

- exact PR-branch build run: `34476518691` — SUCCESS on Ubuntu, Windows, and macOS
- validation-only branch: `validation-watch-companion-tests-20260910`
- validation run: `34476596256` — SUCCESS
- validation command: `cargo test -p isideload --lib`
- tests and build succeeded on Ubuntu, Windows, and macOS
- validation-only workflow modification is not part of PR #12

HealthKit-specific capability handling was intentionally removed from PR #12 so the upstream review stays scoped to generic Watch companion provisioning/signing/install behavior.

### Current upstream review/check state

At this checkpoint:

- PR #12 is Ready for review and publicly visible upstream;
- no requested reviewer is recorded;
- contributor-side attempt to explicitly request `nab138` as reviewer was rejected by GitHub permissions (`RequestReviewsByLogin`);
- this does not invalidate or block the PR itself;
- no maintainer comments, inline review threads, approvals, or change requests have been observed yet;
- upstream workflow run `34478405163` currently reports `action_required` on the PR head SHA;
- treat that as awaiting upstream authorization for the external-fork workflow, not as a source-code test failure.

Do not claim that the upstream CI has passed until that specific upstream PR workflow actually runs and succeeds.

## Scope of PR #12

The PR is intentionally limited to embedded Apple Watch companion support:

- recursive Watch/nested bundle discovery;
- coherent host/Watch identifier rewriting;
- watchOS developer-service request handling;
- paired Watch registration;
- Watch provisioning-profile acquisition;
- nested Watch signing;
- companion-proxy forwarding;
- direct Watch installation through the validated service path;
- focused unit coverage for Watch request/bundle-rewrite behavior.

Do not broaden PR #12 with unrelated dependency/auth/certificate work or HealthKit-specific capability behavior unless upstream review explicitly asks for it.

## What is NOT proven

Do not claim universal support for:

- every iOS/watchOS version or Apple device;
- every entitlement/capability;
- every nested Watch/extension topology;
- independent Watch-only apps;
- App Store/TestFlight distribution;
- arbitrary malformed IPA repair.

The clean PR SHA `a45cf326...` is CI/test validated, but has not yet been separately re-run through the physical-device install path after removing the HealthKit-specific provisioning code. Physical validation belongs to the preserved historical regression pair above.

## Security / privacy rules

Never commit:

- Apple credentials, account/session tokens, or anisette material;
- signing certificates/private keys or `.p12`/`.pem` files;
- provisioning profiles;
- pairing records;
- real UDIDs/device identifiers;
- unredacted private installation logs;
- Health, GPS, workout, or other personal application data;
- local application-project paths or application-specific bundle identifiers unless sanitized as examples.

Use generic examples such as `com.example.host` and `com.example.host.watchkitapp`.

## Current documentation to read before future work

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
- public issue `#1`
- upstream PR `nab138/isideload#12`

## Next exact step

1. Do not make speculative changes to PR #12 while there is no upstream feedback.
2. Re-check PR #12 when the user returns with a notification/comment or explicitly asks for status.
3. If upstream approves the fork workflow, verify the exact upstream run and its result before claiming CI success.
4. If the maintainer comments or requests changes, read the exact discussion/diff first, then modify only the PR branch as needed.
5. Preserve `f7b9f3da...` and `70f37e9b...` as physical regression anchors throughout review.
6. Do not merge PR #12 or publish a release without explicit user approval.
7. Keep HealthKit capability handling outside PR #12 unless the maintainer explicitly asks for it.
8. Prepare the matching iLoader upstream PR only after the isideload backend review shape is stable enough to target.

## Do not do automatically

- do not merge either fork into `main`;
- do not merge upstream PR #12;
- do not publish a release/crate/installer;
- do not delete or rewrite known-good regression anchors;
- do not copy the Watch Tracker app into this repository;
- do not claim upstream endorsement;
- do not open the iLoader upstream PR before the backend review shape is understood.
