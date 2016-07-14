FROM golang:1.6

ENV GOPATH /minio
ENV PATH /minio/bin/:$PATH
ENV SHA256 40cd2faf5dd9503c20d2f5a5ad67277e960561fca5869a9d724d1efa763021df

ENV MINIO_ACCESS_KEY ""
ENV MINIO_SECRET_KEY ""
ENV MINIO_CACHE_SIZE "8g"
ENV MINIO_CACHE_EXPIRY "72h"

WORKDIR /minio/

RUN curl -fsSL "https://github.com/minio/minio/archive/RELEASE.2016-07-13T21-46-05Z.tar.gz" -o minio.tar.gz && \
    echo "$SHA256 minio.tar.gz" | sha256sum -c - && \
    mkdir -p $GOPATH/src/github.com/minio/minio/ && \
    find /minio/ && \
    tar -C $GOPATH/src/github.com/minio/minio/ --strip-components=1 -xzf minio.tar.gz && \
    find /minio/ && \
    rm minio.tar.gz && \
    cd $GOPATH/src/github.com/minio/minio/ && go build -o /minio/bin/minio

VOLUME /minio/config/
VOLUME /minio/data/

EXPOSE 9000

CMD ["bin/minio", "-C", "/minio/config", "server", "--address", ":9000", "/minio/data/"]

