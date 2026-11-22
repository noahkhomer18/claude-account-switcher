# Packaging

## winget

`winget/manifests/` mirrors the layout of [microsoft/winget-pkgs](https://github.com/microsoft/winget-pkgs).
To publish a release:

1. Copy the version folder, bump `PackageVersion`, `ReleaseDate`, the URLs and `InstallerSha256`
   (the hash is in the release's `.sha256` file, upper case).
2. Check it locally:
   ```bash
   winget validate packaging/winget/manifests/s/SnlperStripes/ClaudeAccountSwitcher/<version>
   ```
3. Open a pull request to microsoft/winget-pkgs with the same folder, or let
   [`wingetcreate update`](https://github.com/microsoft/winget-create) do steps 1 and 3.

## Scoop

`scoop/claude-account-switcher.json` is a [Scoop](https://scoop.sh) manifest that installs the Windows build
as the command `claude-account-switcher`. Users install it straight from this repository:

```powershell
scoop install https://raw.githubusercontent.com/SnlperStripes/claude-account-switcher/main/packaging/scoop/claude-account-switcher.json
```

To bump it after a release, set `version`, the `url` and `hash` (lower case, from the release's `.sha256`
file) by hand, or let Scoop do it from `checkver` and `autoupdate`, run from a clone of
[ScoopInstaller/Scoop](https://github.com/ScoopInstaller/Scoop):

```powershell
.\bin\checkver.ps1 -App claude-account-switcher -Dir <this repo>\packaging\scoop -Update
```

Then check that it installs: `scoop install .\packaging\scoop\claude-account-switcher.json`.
