FROM 2020ip/dotnet-mono:latest
MAINTAINER Jarrod Alexander <jarroda@2020research.com>

# Install libuv for Kestrel from source code (binary is not in wheezy and one in jessie is still too old)
# Combining this with the uninstall and purge will save us the space of the build tools in the image

RUN LIBUV_VERSION=1.4.2 \
	&& apt-get update \
	&& apt-get -qqy install libc6-dev libicu-dev autoconf automake build-essential libtool \
    && curl -sSL https://github.com/libuv/libuv/archive/v${LIBUV_VERSION}.tar.gz | tar zxfv - -C /usr/local/src \
    && cd /usr/local/src/libuv-$LIBUV_VERSION \
    && sh autogen.sh && ./configure && make && make install \
    && rm -rf /usr/local/src/libuv-$LIBUV_VERSION \
    && ldconfig \
    && apt-get -y purge autoconf automake build-essential libtool \
    && apt-get -y autoremove \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Prevent `dnu restore` from stalling (gh#63, gh#80)
ENV MONO_THREADS_PER_CPU 50
COPY project.json /package_profiles/
WORKDIR /package_profiles

RUN ["dotnet", "restore"]