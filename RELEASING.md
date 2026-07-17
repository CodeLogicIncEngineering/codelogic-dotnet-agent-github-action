# Releasing this GitHub Action

Follow the common GitHub Actions major-tag convention so consumers can pin `@v1`.

## Steps for each release

1. Merge the change to the default branch (`master`).
2. Create a full version tag and GitHub Release, for example:

   ```bash
   git tag -a v1.0.2 <commit> -m "v1.0.2: <summary>"
   git push origin v1.0.2
   gh release create v1.0.2 --title "v1.0.2" --notes "<summary>"
   ```

3. Move the major tag `v1` to the same commit (delete and recreate if it already exists):

   ```bash
   git tag -d v1
   git push origin :refs/tags/v1
   git tag -a v1 <commit> -m "v1: points to v1.0.2"
   git push origin v1
   ```

## Do not

- Put `${{ github.* }}` or `${{ job.* }}` expressions in `action.yml` input **descriptions** or **defaults**. GitHub evaluates them when loading the action and the workflow will fail to start.
- Leave `v1` pointing at an older commit after cutting a new `v1.x.y` release.
