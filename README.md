# MODFLOW 6 stranded mass preview build

Developmode builds of the `stranded-mass-preview` branch of
[jdhughes-dev/modflow6](https://github.com/jdhughes-dev/modflow6/tree/stranded-mass-preview),
which combines three MODFLOW 6 pull requests that have not been merged:

- [#3056](https://github.com/MODFLOW-ORG/modflow6/pull/3056), the previous saturation for sorbed mass
- [#2918](https://github.com/MODFLOW-ORG/modflow6/pull/2918), stranded mass in the MST Package
- [#3043](https://github.com/MODFLOW-ORG/modflow6/pull/3043), stranded mass in lakes and stream reaches

The build uses the MODFLOW 6 release workflow in developmode, as the
[MODFLOW 6 nightly build](https://github.com/MODFLOW-ORG/modflow6-nightly-build) does:
binaries for Linux and Windows built with the Intel classic compiler, binaries for
macOS on Apple silicon built with gfortran, the tests, and the documentation.
Each build is posted under [Releases](../../releases); the last 10 are kept.

The extended Windows build (parallel and NetCDF) is left out. To do that, the
workflow calls a copy of `.github/workflows/release.yml` from the branch with
the extended entries removed from the build and distribution matrices. If the
release workflow on the branch changes, refresh the copy:

```shell
git -C ../modflow6 show origin/stranded-mass-preview:.github/workflows/release.yml > .github/workflows/release.yml
```

and remove the two `extended: true` matrix entries again.

The workflow runs nightly and builds only when the branch has changed since the
last release. Run it by hand from the Actions tab, with `force` to rebuild an
unchanged branch.

These builds are provisional and are not MODFLOW 6 releases.

## Updating the branch

The three pull requests are stacked, so the head of #3043 contains all three.
After any of them changes:

```shell
git fetch origin
git push --force origin origin/feat-apt-stranded-mass:refs/heads/stranded-mass-preview
```
