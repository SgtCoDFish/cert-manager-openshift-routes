# Releases

## Schedule

The release schedule for this project is ad-hoc. Given the pre-1.0 status of the project we do not have a fixed release cadence. However if a vulnerability is discovered we will respond in accordance with our [security policy](https://github.com/cert-manager/community/blob/main/SECURITY.md) and this response may include a release.

## Process

There is a semi-automated release process for this project. When you create a Git tag with a tagname that has a `v` prefix and push it to GitHub it will trigger the [release workflow].

The release process for this repo is documented below:

1. Create a tag for the new release:
    ```sh
   export VERSION=v0.5.0-alpha.0
   git tag --annotate --message="Release ${VERSION}" "${VERSION}"
   git push origin "${VERSION}"
   ```
2. A GitHub action will see the new tag and do the following:
    - Build and publish any container images
    - Build and bundle the Helm chart
    - Create a draft GitHub release
    - Upload the Helm chart tarball to the GitHub release
3. Once the draft GitHub release has been created, download and test the resulting Helm chart.
4. Create a PR in the [jetstack/jetstack-charts repository on GitHub](https://github.com/jetstack/jetstack-charts), containing the Helm chart file that is attached to the draft GitHub release. This is only currently possible for maintainers inside Venafi, but will be changed in the future.
5. Wait for the PR to be merged and verify that the Helm chart is available from https://charts.jetstack.io.
6. Visit the [releases page], edit the draft release, click "Generate release notes", then edit the notes to add the following to the top
    ```
    approver-policy provides a policy engine for certificates issued by cert-manager!
    ```
7. Publish the release.

## Artifacts

This repo will produce the following artifacts each release. For documentation on how those artifacts are produced see the "Process" section.

- *Container Images* - Container images for the are published to . 
- *Helm chart* - An official Helm chart is maintained within this repo and published to `charts.jetstack.io` on each release.

[release workflow]: https://github.com/cert-manager/approver-policy/actions/workflows/release.yaml
[releases page]: https://github.com/cert-manager/approver-policy/releases