FROM postgres:15

MAINTAINER Neio Zhou <neio.zhou@gmail.com>

ENV PLV8_VERSION=3.1.6 \
    PLV8_SHASUM="136b06db2663a09f46763252171af3e20fe8e1f70282c38bdc6e2239c5596de0"

RUN \
    --mount=type=cache,target=/var/cache/apt \
    buildDependencies="build-essential \
    ca-certificates \
    curl \
    wget \
    git-core \
    python \
    gpp \
    cpp \
    pkg-config \
    apt-transport-https \
    cmake \
    libc++-dev \
    libc++abi-dev \
    libtinfo5 \
    libglib2.0-dev \
    ninja-build \
    postgresql-server-dev-$PG_MAJOR" \
  && runtimeDependencies="libc++1 \
    libtinfo5 \
    libc++abi1" \
  && apt-get update \
  && apt-get install --no-install-recommends -y postgresql-${PG_MAJOR}-ip4r \
  && apt-get install -y --no-install-recommends ${buildDependencies} ${runtimeDependencies}
RUN \
  mkdir -p /tmp/build \
  && curl -o /tmp/build/v$PLV8_VERSION.tar.gz -SL "https://github.com/plv8/plv8/archive/v${PLV8_VERSION}.tar.gz" \
  && cd /tmp/build \
  && echo $PLV8_SHASUM v$PLV8_VERSION.tar.gz | sha256sum -c \
  && tar -xzf /tmp/build/v$PLV8_VERSION.tar.gz -C /tmp/build/ \
  && cd /tmp/build/plv8-$PLV8_VERSION \
  && make static \
  && make install \
  && strip /usr/lib/postgresql/${PG_MAJOR}/lib/plv8-${PLV8_VERSION}.so \
  && rm -rf /root/.vpython_cipd_cache /root/.vpython-root \
  && apt-get clean \
  && apt-get remove -y ${buildDependencies} \
  && apt-get autoremove -y \
  && rm -rf /tmp/build /var/lib/apt/lists/*
