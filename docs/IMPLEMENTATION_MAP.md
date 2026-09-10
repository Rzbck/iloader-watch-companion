# Implementation map

This document maps the physically validated result to the two source repositories and separates **regression anchors** from future **review branches**.

## Regression anchors

### iLoader

- fork: `Rzbck/iloader`
- feature branch: `feat/watch-companion-support-20260909`
- physically validated source revision: `70f37e9b4afc659ab44ec1944c034093f4cda416`
- CI run: `34436587217` — `SUCCESS`
- current feature-branch HEAD at the time of this document: `cd5d1dc55824d4f6929675b445cc7e533e96d8e5`
- commits after the validated source revision are documentation-only at this checkpoint.

Primary implementation ownership visible in the validated branch includes:

- `src-tauri/Cargo.toml` — pin/integrate the matching isideload revision;
- `src-tauri/src/device.rs` — preserve the selected usbmux device/transport context;
- `.github/workflows/build.yml` — allow slash-named feature branches to build.

The historical HANDOFF files are regression/debug documentation and are not intended to be proposed upstream as product source changes.

### isideload

- fork: `Rzbck/isideload`
- feature branch: `feat/watch-companion-support-20260909`
- physically used source revision: `f7b9f3da570edd6824c29680545e710846d07df5`
- CI run: `34436382782` — `SUCCESS`
- current feature-branch HEAD at the time of this document: `5fdc15fa10de927b9fcd962eba4f97bb46e3e44e`
- commits after the validated source revision are documentation-only at this checkpoint.

Watch-related implementation areas in the historical branch include:

- `isideload/src/dev/app_ids.rs` — App ID/capability handling;
- `isideload/src/dev/device_type.rs` — device/platform typing needed for Watch provisioning;
- `isideload/src/dev/devices.rs` — device registration handling;
- `isideload/src/sideload/application.rs` — application/install orchestration;
- `isideload/src/sideload/bundle.rs` — nested app-ID-bearing bundle discovery and bundle relationship handling;
- `isideload/src/sideload/sideloader.rs` — provisioning/signing flow integration;
- `isideload/src/sideload/sign.rs` — signing behavior;
- `isideload/src/sideload/watch_install.rs` — paired-Watch installation path.

## Why the historical branches are not PR branches

The branches were developed while diagnosing a real device-installation failure and intentionally preserve the experiments that led to the working solution.

At this checkpoint:

- the iLoader regression branch has diverged from its current `main` and contains historical documentation in addition to the small integration changes;
- the isideload regression branch has also diverged and includes a broad diff across lockfile/dependency/auth/certificate and sideloading areas in addition to the Watch work.

That history is useful for regression and root-cause evidence, but it is not an appropriate review surface for upstream maintainers.

## Review-branch rule

Future upstream work must use **new cleanup/review branches** based on the relevant current upstream base.

Do not rewrite, force-push, squash away, or delete the known-good regression anchors.

The cleanup process should:

1. identify the minimum Watch-specific behavior needed from the regression branch;
2. reproduce it on a fresh upstream-compatible branch;
3. omit historical HANDOFF/debug-only files from the PR;
4. keep unrelated dependency/auth/certificate changes out unless they are demonstrably required;
5. add or retain focused tests;
6. run exact-SHA CI;
7. perform a sanitized diff/security review;
8. compare behavior back to the known-good hardware anchors when practical.

## Validation evidence

- iLoader workflow run `34436587217` completed successfully for SHA `70f37e9b4afc659ab44ec1944c034093f4cda416`.
- isideload workflow run `34436382782` completed successfully for SHA `f7b9f3da570edd6824c29680545e710846d07df5`.
- the matching pair was then used in the physical Windows → iPhone → paired Apple Watch installation path that completed and launched on both devices.

CI success alone is not the physical evidence; the hardware result is tracked separately in this repository's compatibility documentation and HANDOFF.
