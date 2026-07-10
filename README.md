# catalog-images

Custom-built container images for the [catalog](https://github.com/vojtechmares)
project. These are the general-purpose, open images used by the charts in
[`catalog-charts`](https://github.com/vojtechmares/catalog-charts).

For the premium, minimal, CVE-reduced variants see
[`catalog-hardened-images`](https://github.com/vojtechmares/catalog-hardened-images).

> Status: early scaffolding. The `example` image is a template only.

## Layout

Each image lives in its own top-level directory containing a `Dockerfile` and a
`metadata.yaml`:

```
example/
  Dockerfile
  metadata.yaml     # { image: <name>, version: <tag> }
```

The build workflow discovers every directory with a `Dockerfile`, reads its
`metadata.yaml`, and builds the images that changed.

## Adding an image

1. Copy `example/` to `<your-image>/`.
2. Edit the `Dockerfile` (pin the base image, run as non-root, keep it minimal).
3. Set `image` and `version` in `metadata.yaml`.
4. Open a PR - CI builds the image (without pushing). Merging to `main` builds,
   pushes, signs (cosign) and scans (Trivy) it.

## Published images

Images are published as OCI artifacts to:

```
registry.mareshq.com/catalog/images/<image>:<version>
```

They are multi-arch (`linux/amd64`, `linux/arm64`), signed with cosign, and ship
with SBOM and provenance attestations.

### Verifying

```sh
cosign verify \
  --certificate-identity-regexp '^https://github.com/vojtechmares/catalog-images' \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com \
  registry.mareshq.com/catalog/images/<image>:<version>
```

## License

[Apache-2.0](./LICENSE).
