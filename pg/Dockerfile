FROM bitnami/postgresql-repmgr:11

USER root
RUN sudo mkdir -p /var/lib/apt/lists/partial

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    postgresql-server-dev-11 \
    gcc \
    make \
    libc-dev \
    g++ \
    git \
    cmake \
    curl \
    ca-certificates \
    openssl \
  && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/jaiminpan/pg_jieba \
  && cd /pg_jieba \
  && git submodule update --init --recursive

RUN cd /pg_jieba \
  && mkdir -p build \
  && cd build \
  && curl -L https://raw.githubusercontent.com/Kitware/CMake/ce629c5ddeb7d4a87ac287c293fb164099812ca2/Modules/FindPostgreSQL.cmake > $(find /usr -name "FindPostgreSQL.cmake") \
  && cmake -DPostgreSQL_TYPE_INCLUDE_DIR=/usr/include/postgresql/11/server .. \
  && make \
  && make install \
  && apt-get purge -y gcc make libc-dev postgresql-server-dev-11 g++ git cmake curl\
  && apt-get autoremove -y \
  && rm -rf /pg_jieba

USER 1001
