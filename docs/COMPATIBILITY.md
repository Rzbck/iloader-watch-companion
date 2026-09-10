# Compatibility and validation

## Known-good regression pair

| Component | Revision | Evidence |
| --- | --- | --- |
| iLoader | `70f37e9b4afc659ab44ec1944c034093f4cda416` | Physical iPhone + paired Watch installation/launch validated |
| isideload | `f7b9f3da570edd6824c29680545e710846d07df5` | Backend used by the physically validated iLoader build |

## Confirmed behavior

The tested Windows-driven flow demonstrated:

- iPhone host installation;
- iPhone host launch;
- discovery of the embedded Watch companion;
- Watch-target provisioning;
- explicit Watch signing;
- installation on the paired physical Apple Watch;
- Watch companion launch.

The physical test application also exercised HealthKit-capability provisioning through the same signing path.

## Not yet generalized

Current evidence does **not** prove support for:

- every iOS or watchOS release;
- every iPhone or Apple Watch model;
- every entitlement/capability combination;
- every nested extension/watch bundle topology;
- App Store or TestFlight distribution;
- repair of arbitrary malformed IPAs;
- independent Watch apps without an iPhone host.

## Validation vocabulary

Use these labels precisely:

- `BUILD_VALIDATED`
- `CI_VALIDATED`
- `PACKAGED`
- `IPHONE_INSTALLED`
- `IPHONE_LAUNCHED`
- `WATCH_INSTALLED`
- `WATCH_LAUNCHED`
- `PHYSICALLY_VALIDATED`

Do not call simulator, compile, CI, or packaging evidence `PHYSICALLY_VALIDATED`.

## Adding compatibility evidence

When testing another environment, record only information needed to reproduce the result:

- iLoader revision;
- isideload revision;
- host OS family/version;
- iOS/watchOS versions;
- relevant capability class;
- success/failure stage;
- sanitized error/log excerpt when needed.

Do not publish UDIDs, Apple account data, signing identities, certificates, provisioning profiles, or pairing records.
