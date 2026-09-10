# Apple Watch Companion Support for iLoader

Experimental Apple Watch companion sideloading support for the [iLoader](https://github.com/nab138/iloader) / [isideload](https://github.com/nab138/isideload) stack.

> **Independent community work.** This repository is not an official iLoader release and is not affiliated with or endorsed by the iLoader maintainers. The official iLoader project is available at [iloader.app](https://iloader.app) and [github.com/nab138/iloader](https://github.com/nab138/iloader).

## Status

A Windows-driven path for installing an iPhone IPA with an embedded watchOS companion has been **physically validated** on a real iPhone and paired Apple Watch.

Known-good regression anchors:

- iLoader: `70f37e9b4afc659ab44ec1944c034093f4cda416`
- isideload: `f7b9f3da570edd6824c29680545e710846d07df5`

The validated flow installed and launched both the iPhone host app and the embedded Watch companion. This does **not** imply universal compatibility with every iOS/watchOS version, device model, entitlement, IPA topology, or signing configuration.

## What was added

The working path covers the parts that a normal iPhone-only sideload flow does not fully handle:

- recursive discovery of app-ID-bearing nested bundles;
- coherent rewriting of host/Watch bundle relationships after sideload identifiers change;
- provisioning the paired Apple Watch as a target device;
- obtaining and embedding appropriate provisioning profiles for Watch bundles;
- explicit signing of the embedded Watch application;
- preserving the selected usbmux transport/device context;
- establishing the companion-device installation path;
- capability-aware provisioning used by the physically tested HealthKit application.

## Where the implementation lives

The implementation remains in the repositories that own each responsibility:

| Project | Role | Working branch | Known-good revision |
| --- | --- | --- | --- |
| [`Rzbck/isideload`](https://github.com/Rzbck/isideload) | IPA graph discovery, provisioning, identifier rewriting and signing | `feat/watch-companion-support-20260909` | `f7b9f3da570edd6824c29680545e710846d07df5` |
| [`Rzbck/iloader`](https://github.com/Rzbck/iloader) | Desktop integration, transport preservation and companion installation orchestration | `feat/watch-companion-support-20260909` | `70f37e9b4afc659ab44ec1944c034093f4cda416` |

This repository intentionally does **not** vendor complete copies of those projects. It is the clean public entry point for architecture, validation, security guidance, and upstream review status.

## Documentation

- [Architecture](docs/ARCHITECTURE.md)
- [Compatibility and validation](docs/COMPATIBILITY.md)
- [Testing](docs/TESTING.md)
- [Upstream contribution plan](docs/UPSTREAM.md)
- [Security policy](SECURITY.md)
- [Contributing](CONTRIBUTING.md)
- [Attribution and trademark notice](NOTICE.md)
- [Project handoff](HANDOFF.md)

## Upstream direction

The intended contribution sequence is:

1. reduce the `isideload` changes to a clean, generic patch;
2. run its tests/CI and preserve the known-good hardware regression anchor;
3. open a draft PR against `nab138/isideload`;
4. incorporate maintainer review;
5. clean the smaller iLoader integration against the backend shape under review;
6. open the matching draft PR against `nab138/iloader`.

No upstream merge or release is implied by this repository.

## Security and privacy

Do not commit Apple credentials, certificates, private keys, provisioning profiles, pairing records, real device UDIDs, Health/GPS data, or unredacted installation logs. See [SECURITY.md](SECURITY.md).

## License

The documentation and original material in this repository are licensed under the MIT License. iLoader and isideload remain governed by their respective upstream licenses and notices. The iLoader name, logos, and other branding are subject to the upstream project's separate branding terms; see [NOTICE.md](NOTICE.md).
