# -*- mode: dockerfile; coding: utf-8 -*-
FROM schemers/chicken AS build
RUN apt-get update && apt-get -y --no-install-recommends install \
      git ca-certificates \
      build-essential \
 && rm -rf /var/lib/apt/lists/*
WORKDIR /build
RUN git clone https://code.call-cc.org/git/chicken-core.git chicken --depth 1
WORKDIR /build/chicken
RUN make PLATFORM=linux spotless
RUN make PLATFORM=linux CHICKEN=/usr/local/bin/chicken
RUN make PLATFORM=linux install
RUN chicken-install r7rs

FROM debian:buster-slim
RUN apt-get update && apt-get -y --no-install-recommends install \
      gcc libc-dev \
 && rm -rf /var/lib/apt/lists/*
COPY --from=build /usr/local/ /usr/local/
CMD ["scheme-banner"]
