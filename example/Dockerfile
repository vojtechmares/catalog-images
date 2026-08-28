# Reference image / template. Copy this directory to add a new image.
#
# Guidelines:
#   - pin the upstream base image by tag (and ideally digest)
#   - run as a non-root user
#   - keep the final image minimal
#   - keep the version in metadata.yaml in sync with the base image
FROM nginxinc/nginx-unprivileged:1.31.4-alpine

# OCI image labels (also injected by CI via docker/metadata-action).
LABEL org.opencontainers.image.source="https://github.com/vojtechmares/catalog-images" \
      org.opencontainers.image.description="Example catalog image (unprivileged nginx)" \
      org.opencontainers.image.licenses="Apache-2.0"

USER 101
