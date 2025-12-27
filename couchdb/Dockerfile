# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile

# Global build argument
ARG BUILD_FROM

# Get CouchDB from official image
FROM couchdb:3.3 AS couchdb

# Main build
FROM $BUILD_FROM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install glibc to run Debian-compiled CouchDB binaries
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
    && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.35-r1/glibc-2.35-r1.apk \
    && apk add --no-cache --force-overwrite glibc-2.35-r1.apk \
    && rm glibc-2.35-r1.apk

# Install requirements for add-on
RUN \
    apk add --no-cache \
    bash \
    curl \
    su-exec \
    tini \
    openssl \
    icu-libs \
    libstdc++ \
    libgcc \
    dos2unix

# Copy CouchDB from official image
COPY --from=couchdb /opt/couchdb /opt/couchdb

# Fix glibc loader path - Debian binaries expect it in /lib64
RUN mkdir -p /lib64 \
    && ln -sf /usr/glibc-compat/lib/ld-linux-aarch64.so.1 /lib64/ld-linux-aarch64.so.1 2>/dev/null || true \
    && ln -sf /usr/glibc-compat/lib/ld-linux-x86-64.so.2 /lib64/ld-linux-x86-64.so.2 2>/dev/null || true

# Create CouchDB user and set permissions
RUN \
    addgroup -g 5984 couchdb \
    && adduser -u 5984 -G couchdb -s /bin/bash -D couchdb \
    && mkdir -p /opt/couchdb/data /opt/couchdb/etc/local.d /opt/couchdb/var/log \
    && chown -R couchdb:couchdb /opt/couchdb

# Copy root filesystem
COPY rootfs /

# Set proper permissions for service scripts and fix line endings
RUN \
    dos2unix /etc/services.d/couchdb/run /etc/services.d/couchdb/finish || true \
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