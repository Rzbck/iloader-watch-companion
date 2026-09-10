# Architecture

## Core idea

An IPA with an embedded Apple Watch companion must be handled as a **bundle graph**, not as one iPhone application.

```text
IPA
└── Payload/Host.app
    ├── host bundle identifier
    ├── host provisioning/signature
    └── Watch/Companion.app
        ├── Watch bundle identifier
        ├── companion relationship
        ├── Watch provisioning profile
        └── Watch signature
```

A successful sideload must keep identifiers, provisioning, signatures, and device targets coherent across that graph.

## Validated high-level flow

```text
Read IPA
  ↓
Discover app-ID-bearing bundles recursively
  ↓
Resolve sideload identifiers
  ↓
Rewrite dependent host/companion relationships
  ↓
Register/provision host + embedded targets
  ↓
Sign nested Watch content and host in a valid order
  ↓
Install iPhone host
  ↓
Resolve paired Apple Watch companion path
  ↓
Install Watch companion
```

## Responsibility split

### isideload

The backend owns generic IPA/signing/provisioning concerns:

- recursive bundle discovery;
- App ID/profile requirements for nested bundles;
- dependent identifier rewriting;
- Watch-target provisioning decisions;
- capability-aware provisioning;
- nested Watch signing.

### iLoader

The desktop application owns device-side integration:

- preserving the user-selected device/transport;
- invoking the appropriate isideload backend;
- installing the iPhone host;
- establishing the paired-companion device path;
- triggering Watch installation.

## Design invariants

1. Signing only the parent iPhone bundle is insufficient evidence that an embedded Watch target is valid.
2. Rewritten identifiers must preserve all host/companion relationships.
3. Provisioning is target-specific; a valid iPhone profile does not prove the Watch target is correctly provisioned.
4. Device transport/context must remain associated with the device the user selected.
5. Build, CI, package creation, installation, and physical launch are separate validation states.

## Non-goals

This repository does not contain a fitness application, Health/GPS data, real device identifiers, Apple credentials, signing keys, or provisioning profiles.
