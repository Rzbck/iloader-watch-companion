# Repository settings

These settings are part of the intended public-repository configuration.

## Repository presentation

- visibility: public
- default branch: `main`
- issues: enabled
- wiki: disabled
- projects: disabled unless a real project board becomes useful
- delete merged branches automatically: enabled
- allow updating out-of-date PR branches: enabled

Recommended topics:

- `apple-watch`
- `watchos`
- `ios`
- `sideloading`
- `iloader`
- `isideload`
- `windows`
- `apple`

## Merge policy

For this documentation/integration repository:

- squash merge: enabled
- rebase merge: enabled
- merge commits: disabled
- auto-merge: optional; keep disabled until there is a reason to use it

No required status-check rule is defined yet because this repository currently contains documentation rather than executable source/CI. Revisit branch rules if code or automated checks are added here later.

## Security settings

For a public repository, enable when available:

- secret scanning;
- secret scanning push protection;
- vulnerability/dependency alerts;
- private vulnerability reporting.

`SECURITY.md` assumes private vulnerability reporting will be enabled when possible.

## GitHub CLI configuration

Run from an authenticated GitHub CLI session with repository admin permission:

```powershell
& {
    $ErrorActionPreference = 'Stop'
    $Repo = 'Rzbck/iloader-watch-companion'

    gh repo edit $Repo `
        --enable-issues=true `
        --enable-wiki=false `
        --enable-projects=false `
        --delete-branch-on-merge=true `
        --allow-update-branch=true `
        --enable-squash-merge=true `
        --enable-rebase-merge=true `
        --enable-merge-commit=false `
        --enable-secret-scanning=true `
        --enable-secret-scanning-push-protection=true `
        --add-topic apple-watch `
        --add-topic watchos `
        --add-topic ios `
        --add-topic sideloading `
        --add-topic iloader `
        --add-topic isideload `
        --add-topic windows `
        --add-topic apple

    if ($LASTEXITCODE -ne 0) {
        throw 'STOP: repository settings update failed.'
    }

    gh api --method PUT "repos/$Repo/vulnerability-alerts"
    if ($LASTEXITCODE -ne 0) {
        throw 'STOP: vulnerability alerts could not be enabled.'
    }

    gh api --method PUT "repos/$Repo/private-vulnerability-reporting"
    if ($LASTEXITCODE -ne 0) {
        throw 'STOP: private vulnerability reporting could not be enabled.'
    }

    gh repo view $Repo
}
```

If a security feature is unavailable for the account/repository, record the exact GitHub error instead of assuming it is enabled.
