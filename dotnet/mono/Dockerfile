FROM microsoft/dotnet:1.0.0-preview1
MAINTAINER Jarrod Alexander <jarroda@2020research.com>

ENV PREFIX=/usr/local

RUN apt-get update \
	&& apt-get install -y unzip patch git autoconf libtool libtool-bin automake build-essential gettext \
	&& rm -rf /var/lib/apt/lists/*

RUN PATH=$PREFIX/bin:$PATH \
    git clone --recursive https://github.com/mono/mono.git \
    && cd mono \
    git checkout tags/mono-4.4.0.148 \
    && wget -q -O - https://patch-diff.githubusercontent.com/raw/mono/mono/pull/2771.patch | patch -p1 --merge \
    && ./autogen.sh --prefix=$PREFIX \
    && make get-monolite-latest \
    && make \
    && make install \
    && cd .. \
    && rm -rf mono