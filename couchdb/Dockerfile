# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile

ARG BUILD_FROM
FROM couchdb:3.3 AS couchdb

# Main build
FROM $BUILD_FROM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install runtime dependencies that CouchDB needs
RUN apk add --no-cache \
    bash \
    curl \
    dos2unix \
    libstdc++ \
    libgcc \
    ncurses-libs \
    openssl

# Copy CouchDB completely from official image
COPY --from=couchdb /opt/couchdb /opt/couchdb

# Copy necessary system libraries and dependencies from Debian image
COPY --from=couchdb /lib/x86_64-linux-gnu/*.so* /lib/ 2>/dev/null || true
COPY --from=couchdb /lib/aarch64-linux-gnu/*.so* /lib/ 2>/dev/null || true
COPY --from=couchdb /usr/lib/x86_64-linux-gnu/*.so* /usr/lib/ 2>/dev/null || true
COPY --from=couchdb /usr/lib/aarch64-linux-gnu/*.so* /usr/lib/ 2>/dev/null || true

# Create CouchDB user and set permissions
RUN addgroup -g 5984 couchdb \
    && adduser -u 5984 -G couchdb -s /bin/bash -D couchdb \
    && mkdir -p /opt/couchdb/data /opt/couchdb/etc/local.d /opt/couchdb/var/log \
    && chown -R couchdb:couchdb /opt/couchdb

# Copy root filesystem
COPY rootfs /

# Set proper permissions for service scripts
RUN dos2unix /etc/services.d/couchdb/run /etc/services.d/couchdb/finish || true \
    && chmod +x /etc/services.d/couchdb/run \
    && chmod +x /etc/services.d/couchdb/finish

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="db1996" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Add-ons" \
    org.opencontainers.image.authors="db1996" \
    org.opencontainers.image.licenses="Apache License 2.0" \
    org.opencontainers.image.url="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}