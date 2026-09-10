# Upstream contribution plan

## Why the work is split

The Apple Watch companion path crosses two upstream projects with different responsibilities:

- `isideload`: generic IPA graph, provisioning, capability and signing behavior;
- `iLoader`: desktop/device integration and companion installation orchestration.

Keeping those reviews separate makes each patch smaller and easier to reason about.

## 1. isideload first

Fork: `Rzbck/isideload`

Working branch: `feat/watch-companion-support-20260909`

Known-good regression anchor:

`f7b9f3da570edd6824c29680545e710846d07df5`

Before opening a PR:

1. fetch the current upstream base;
2. inspect the complete feature diff;
3. separate generic Watch support from historical diagnostics/documentation;
4. remove application-specific assumptions and local-environment residue;
5. preserve or add focused tests;
6. run the repository's CI/tests;
7. re-check security/privacy of the diff;
8. open a **draft PR** against `nab138/isideload`.

Do not rewrite the known-good hardware anchor merely to create cleaner history. Use a separate cleanup/review branch if needed.

## 2. iLoader second

Fork: `Rzbck/iloader`

Working branch: `feat/watch-companion-support-20260909`

Known-good regression anchor:

`70f37e9b4afc659ab44ec1944c034093f4cda416`

The iLoader review should be prepared after the backend API/shape is stable enough to reference. Keep only the integration changes that actually belong in iLoader.

Target upstream: `nab138/iloader`.

## PR posture

A pull request is a proposal for review; it does not merge code automatically. Keep the first submission as a draft while cleanup or validation remains.

Each PR description should state:

- problem and user-visible motivation;
- architecture/ownership of the fix;
- exact tests and CI results;
- exact hardware validation performed, if any;
- known limitations;
- dependency on the companion PR, if applicable.

## Review feedback workflow

For every maintainer request:

1. identify which repository owns the requested behavior;
2. make the smallest relevant change;
3. run the appropriate tests/CI;
4. record the new SHA;
5. keep source/CI evidence distinct from physical-device validation.

Do not merge upstream, publish releases, or replace the known-good local builds without an explicit decision.
