FROM microsoft/aspnet:1.0.0-rc1-update1
MAINTAINER 2020IP

RUN apt-get update \ 
	&& apt-get install -y \
	curl \
	git-core \
	&& apt-get -y clean \
	&& apt-get -y purge \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
	&& curl -sL https://deb.nodesource.com/setup_4.x | bash - \
	&& apt-get install -y nodejs \
	&& npm install -g bower \
	&& npm install -g gulp

COPY project.json /package_profiles/
WORKDIR /package_profiles
RUN ["dnu", "restore"]
