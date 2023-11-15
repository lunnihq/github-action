# `lunni/github-action`

Build Docker image and update it on a Lunni server.


## Usage

```yaml
name: Push into main branch
on:
  push:
    branches: ["master"]

jobs:
  context:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Build
        id: build
        uses: lunnihq/github-action@main
        with:
          password: ${{ secrets.GITHUB_TOKEN }}
          lunni-webhook-url: "${{ env.LUNNI_WEBHOOK_URL }}"

    outputs:
      image: ${{ steps.build.outputs.image }}
      tag: ${{ steps.build.outputs.tag }}
```


## Inputs

| Name | Description |
|------|-------------|
| `context` | Build's context is the set of files located in the specified PATH or URL |
| `file` | Path to the Dockerfile |
| `image_name` | Image name (excluding registry). Defaults to `${{ github.repository }}`. |
| `registry` | Docker registry. Defaults to ghcr.io. |
| `username` | Docker username. Defaults to `${{ github.actor }}`. |
| `password` | Docker password. Set this to `${{ secrets.GITHUB_TOKEN }}` if publishing to GHCR. |
| `lunni-webhook-url` | Lunni service webhook |
| `build-args` | List of build-time variables |
| `cache-from` | List of external cache sources for buildx (e.g., user/app:cache, type=local,src=path/to/dir) |
| `cache-to` | List of cache export destinations for buildx (e.g., user/app:cache, type=local,dest=path/to/dir) |
| `platforms` | List of target platforms for build (e.g. linux/amd64,linux/arm64,linux/riscv64,linux/ppc64le,linux/s390x,etc) |
| `provenance` | Generate provenance attestation for the build |
| `ssh` | List of SSH agent socket or keys to expose to the build |
| `tags` | List of tags ([docs](https://github.com/docker/metadata-action#tags-input)) |
| `flavor` | Defines a global behavior for tags: ([docs](https://github.com/docker/metadata-action#flavor-input)1 |
| `target` | Sets the target stage to build |
| `secrets` | List of secrets to expose to the build (e.g., key=string, GIT_AUTH_TOKEN=mytoken) |
| `secret-files` | List of secret files to expose to the build (e.g., key=filename, MY_SECRET=./secret.txt) |
| `docker-metadata-pr-head-sha` | Set to `true` to tag images with the PR HEAD SHA instead of the merge commit SHA within pull requests. |


## Outputs

| Name | Description |
|------|-------------|
| `image` | Docker image name |
| `metadata` | Docker image metadata |
| `tag` | Docker image tag |


## License

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This action is heavily based on [github-action-docker-build-push](https://github.com/cloudposse/github-action-docker-build-push) by Cloud Posse. Check them out!
