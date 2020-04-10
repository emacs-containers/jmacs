FROM debian:buster-slim AS build
RUN apt-get update && apt-get -y --no-install-recommends install \
      libc-dev gcc make \
 && rm -rf /var/lib/apt/lists/*
WORKDIR /build
COPY checksum checksum
ADD https://sourceforge.net/projects/joe-editor/files/JOE%20sources/joe-4.6/joe-4.6.tar.gz/download joe.tar.gz
RUN sha256sum joe.tar.gz && sha256sum -c checksum
RUN mkdir joe && tar -C joe --strip-components 1 -xf joe.tar.gz
WORKDIR /build/joe
RUN ./configure
RUN make
RUN make install

FROM debian:buster-slim
COPY --from=build /usr/local/ /usr/local/
CMD ["jmacs"]
