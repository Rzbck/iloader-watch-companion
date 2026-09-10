# Testing

## Goal

Validate the generic Apple Watch companion sideload path without relying on application-specific identifiers or personal data.

## Test IPA shape

A representative development IPA should contain an iPhone host and embedded Watch application, for example:

```text
Payload/
  ExampleHost.app/
    Watch/
      ExampleWatch.app/
```

Use sanitized identifiers such as:

```text
com.example.host
com.example.host.watchkitapp
```

Never commit generated signing/provisioning material.

## Validation procedure

Record the exact iLoader and isideload revisions before testing.

1. Confirm the IPA contains the expected embedded Watch bundle.
2. Run the iLoader signing/install path.
3. Confirm the iPhone host installs.
4. Confirm the iPhone host launches.
5. Confirm the paired Watch receives the companion app.
6. Confirm installation completes instead of remaining a placeholder.
7. Confirm the Watch app launches.
8. Verify any capability specifically under test.
9. Sanitize logs before publishing them.

## Regression anchors

Known-good pair:

- iLoader `70f37e9b4afc659ab44ec1944c034093f4cda416`
- isideload `f7b9f3da570edd6824c29680545e710846d07df5`

Cleanup/refactor branches may move beyond these SHAs. When behavior regresses, compare against the known-good pair instead of rewriting or rebasing away the evidence.

## Failure reporting

Report the first failing stage precisely. Useful categories include:

- nested bundle not discovered;
- identifier relationship invalid;
- App ID/profile creation failure;
- Watch profile/platform mismatch;
- signing failure;
- iPhone install failure;
- companion transport failure;
- Watch install/integrity failure;
- Watch launch failure.

Do not infer a root cause until the failing layer is identified.
