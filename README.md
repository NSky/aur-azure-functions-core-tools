# aur-azure-functions-core-tools

Source for the AUR package
[`azure-functions-core-tools-bin`](https://aur.archlinux.org/packages/azure-functions-core-tools-bin).

## How updates work

1. **Renovate** watches the `# renovate:` comment on `pkgver` in `PKGBUILD` and
   opens a PR when Azure tags a new release. It only changes `pkgver`.
2. **Check package** (`.github/workflows/check.yml`) runs on that PR: it resets
   `pkgrel` to 1, recomputes `b2sums`, regenerates `.SRCINFO`, builds the
   package, checks `func --version`, and commits the fixed files back to the PR.
3. Review and merge the PR.
4. **Publish to AUR** (`.github/workflows/aur.yml`) runs on `master`: it checks
   `.SRCINFO` matches `PKGBUILD`, copies both into the AUR repo and pushes.
   Only those two files go to the AUR (it rejects subdirectories).

## Setup

- Install the [Renovate GitHub App](https://github.com/apps/renovate) on this repo.
- Add an SSH key dedicated to this repo to your AUR account, and store its
  private half as the `AUR_SSH_PRIVATE_KEY` repository secret.

## Manual changes

Edit `PKGBUILD` (bump `pkgrel` if the package contents change), run
`makepkg --printsrcinfo > .SRCINFO`, commit and push to `master`. The publish
workflow pushes it to the AUR. Don't push to the AUR directly, or the two repos
will diverge.
