# Build image
FROM alpine:3.8 as build

ENV LANG ja_JP.UTF-8
ENV KYOTOCABINET_VERSION 1.2.76
ENV KYOTOTYCOON_VERSION 0.9.56

RUN apk update && apk upgrade
RUN apk --no-cache add libstdc++ lua
RUN apk --no-cache add --virtual build-dependencies build-base zlib-dev curl lua-dev
RUN curl -SLO http://fallabs.com/kyotocabinet/pkg/kyotocabinet-${KYOTOCABINET_VERSION}.tar.gz && \
  tar xzvf kyotocabinet-${KYOTOCABINET_VERSION}.tar.gz
RUN cd kyotocabinet-${KYOTOCABINET_VERSION} && \
  ./configure CFLAGS='-std=c++98' CXXFLAGS='-std=c++98' --enable-static && \
  make && \
  make install
RUN curl -SLO http://fallabs.com/kyototycoon/pkg/kyototycoon-${KYOTOTYCOON_VERSION}.tar.gz && \
  tar xzvf kyototycoon-${KYOTOTYCOON_VERSION}.tar.gz
RUN cd kyototycoon-${KYOTOTYCOON_VERSION} && \
  ./configure CFLAGS='-std=c++98' CXXFLAGS='-std=c++98' --with-kc=/usr/local --enable-lua --enable-static && \
  sed -i -e "/^#include <kttimeddb.h>$/a #include <unistd.h>" ./ktdbext.h && \
  make && \
  make install

# Runtime image
FROM alpine:3.8

RUN apk --no-cache add lua
COPY --from=build /usr/local/bin/* /usr/local/bin/

EXPOSE 1978
ENTRYPOINT ["/usr/local/bin/ktserver"]
