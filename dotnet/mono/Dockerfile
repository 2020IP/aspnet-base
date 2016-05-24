FROM microsoft/dotnet:1.0.0-preview1
MAINTAINER Jarrod Alexander <jarroda@2020research.com>

ENV PREFIX=/usr/local

RUN apt-get update \
	&& apt-get install -y unzip patch autoconf libtool libtool-bin automake build-essential gettext \
	&& rm -rf /var/lib/apt/lists/*

RUN PATH=$PREFIX/bin:$PATH \
    && wget https://github.com/mono/mono/archive/mono-4.4.0.148.zip \
    && unzip mono-4.4.0.148.zip \
    && cd mono-mono-4.4.0.148 \
    && wget -q -O - https://patch-diff.githubusercontent.com/raw/mono/mono/pull/2771.patch | patch -p1 --merge \
    && ./autogen.sh --prefix=$PREFIX \
    && make get-monolite-latest \
    && make \
    && make install \
    && cd .. \
    && rm -rf mono-4.4.0.148.zip \
    && rm -f mono-4.4.0.148.zip