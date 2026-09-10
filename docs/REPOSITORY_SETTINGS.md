# Repository settings

Repository administration was applied and checked on 2026-09-10.

## Verified repository presentation

- visibility: public
- default branch: `main`
- issues: enabled
- wiki: disabled
- projects: disabled
- delete merged branches automatically: enabled
- allow updating out-of-date PR branches: enabled
- license detected by GitHub: MIT

Topics:

- `apple`
- `apple-watch`
- `iloader`
- `ios`
- `isideload`
- `sideloading`
- `watchos`
- `windows`

## Verified merge policy

- squash merge: enabled
- rebase merge: enabled
- merge commits: disabled
- auto-merge: disabled

No required status-check rule is defined yet because this repository currently contains documentation rather than executable source/CI. Revisit branch rules if code or automated checks are added here later.

## Security configuration

The owner CLI configuration command completed successfully for:

- secret scanning;
- secret scanning push protection;
- vulnerability alerts;
- private vulnerability reporting.

The public repository metadata independently confirms the repository/merge/topic settings above. The connected GitHub API used by this project cannot read back the private-vulnerability-reporting endpoint, so preserve the successful owner-CLI result as the configuration evidence unless a later GitHub check shows otherwise.

`SECURITY.md` remains the public disclosure policy and must be kept consistent with the repository security settings.

## Reconfiguration command

If repository administration needs to be restored or audited from an authenticated owner CLI session:

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

Never claim a later security-setting change succeeded unless the command/API operation actually succeeds.
