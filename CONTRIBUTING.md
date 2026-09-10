# Contributing

Thanks for helping improve Apple Watch companion sideloading support around iLoader/isideload.

## Choose the right repository

This repository is the public integration and validation hub. Keep implementation changes in the project that owns them:

- `isideload`: IPA bundle discovery, provisioning, identifier rewriting, capabilities, signing;
- `iLoader`: desktop integration, selected-device transport, companion-device installation orchestration;
- this repository: architecture, compatibility notes, reproducible validation, security guidance, and upstream coordination.

Do not copy unrelated application code into this repository.

## Before opening an issue or pull request

- verify the exact repository, branch, and commit involved;
- separate build/CI success from physical iPhone/Watch validation;
- reproduce against the current relevant branch before changing code;
- compare regressions against the documented known-good revisions;
- remove personal data and secrets from logs and examples.

## Privacy requirements

Never include real Apple credentials, certificates, provisioning profiles, pairing records, UDIDs, Health/GPS data, or unredacted private logs.

Use generic identifiers such as:

```text
com.example.host
com.example.host.watchkitapp
```

## Pull requests

Keep PRs focused. Explain:

1. the problem being solved;
2. which layer owns the fix;
3. the exact tests/CI run;
4. whether real hardware was tested;
5. remaining limitations.

Prefer draft PRs while the implementation is still being cleaned or validated.

## Commit style

Use short imperative/conventional subjects when practical, for example:

```text
fix(watch): preserve companion transport
feat(watch): provision embedded Watch bundles
docs: clarify physical validation matrix
```

## Upstream contributions

The intended order is to review the generic backend changes in `isideload` first, then adapt the smaller iLoader integration to the accepted/proposed backend shape. See `docs/UPSTREAM.md`.
