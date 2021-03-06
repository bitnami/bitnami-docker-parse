FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages acl ca-certificates curl gzip jq libbz2-1.0 libc6 libcom-err2 libcurl4 libffi6 libgcc1 libgcrypt20 libgmp10 libgnutls30 libgpg-error0 libgssapi-krb5-2 libhogweed4 libidn2-0 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 liblzma5 libncursesw6 libnettle6 libnghttp2-14 libp11-kit0 libpsl5 libreadline7 librtmp1 libsasl2-2 libsqlite3-0 libssh2-1 libssl1.1 libstdc++6 libtasn1-6 libtinfo6 libunistring2 procps tar zlib1g
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "python" "3.8.11-0" --checksum 28b91ef5db9ad93e704881400703e4085bd82f016be15e3cf8760df044da9490
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "node" "12.22.3-2" --checksum 6b43b72178f156e5614f4dc91ae6443c7c891c255189cc580ea97a04d02218c2
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "mongodb-client" "4.4.7-0" --checksum b624c290d0d626687b2eeb2a79ff6b59d99da6831d050b892d257c12efa14fe8
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "parse" "4.9.3-1" --checksum 993e3d62564c5b75e651623f9a9dd988992de5b7f98c8a09efd4cf3809cbb678
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.13.0-0" --checksum fd7257c2736164d02832dbf72e2c1ed9d875bf3e32f0988520796bc503330129
RUN chmod g+rwX /opt/bitnami

COPY rootfs /
RUN /opt/bitnami/scripts/parse/postunpack.sh
ENV BITNAMI_APP_NAME="parse" \
    BITNAMI_IMAGE_VERSION="4.9.3-debian-10-r190" \
    PATH="/opt/bitnami/python/bin:/opt/bitnami/node/bin:/opt/bitnami/mongodb/bin:/opt/bitnami/mongodb-client/bin:/opt/bitnami/parse/bin:/opt/bitnami/common/bin:$PATH"

EXPOSE 1337 3000

USER 1001
ENTRYPOINT [ "/opt/bitnami/scripts/parse/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/parse/run.sh" ]
