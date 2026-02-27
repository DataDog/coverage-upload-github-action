# Releasing

## Versioning Strategy

This action follows [semantic versioning](https://semver.org/) with floating major version tags, as recommended by the [GitHub Actions toolkit](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md#recommendations).

Users reference the action by its major version (e.g., `uses: DataDog/coverage-upload-github-action@v2`), which always points to the latest `v2.x.y` release. The floating tag is updated automatically by the [release workflow](.github/workflows/release.yml).

## Release Process

1. Ensure all changes are merged to `main`.
2. Create and push a semver tag:
   ```bash
   git tag v2.0.0
   git push origin v2.0.0
   ```
3. The `release.yml` workflow will automatically:
   - Create a GitHub Release with auto-generated release notes.
   - Update the floating major version tag (`v2`) to point to the new release.
4. Verify the GitHub Release appears at https://github.com/DataDog/coverage-upload-github-action/releases.

## Major Version Releases

Bump the major version when making breaking changes to:

- Action inputs (renaming, removing, or changing required/optional status)
- Action outputs
- Default behavior that users depend on

To release a new major version (e.g., `v3`):

1. Follow the standard release process with the new major version tag (e.g., `v3.0.0`).
2. The workflow will automatically create the new floating tag (`v3`).
3. Update the `README.md` usage examples to reference the new major version.

## Hotfix Process

To patch an older major version:

1. Create a release branch from the last tag of that major version:
   ```bash
   git checkout -b release/v2 v2.1.0
   git push origin release/v2
   ```
2. Cherry-pick or apply the fix on the release branch.
3. Tag and push from the release branch:
   ```bash
   git tag v2.1.1
   git push origin v2.1.1
   ```
4. The workflow will update the `v2` floating tag automatically.
