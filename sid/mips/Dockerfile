# GENERATED from Dockerfile.template. DO NOT EDIT.
FROM vicamo/buildpack-deps:sid-mips

ENV LAARID_USER=laarid
ENV LAARID_HOME=/home/${LAARID_USER}

RUN echo "$(cat /etc/apt/sources.list | sed 's,^deb ,deb-src ,')" >> /etc/apt/sources.list \
	&& apt-get update -qq \
	&& apt-get upgrade -y \
	&& apt-get install --no-install-recommends -y \
		build-essential \
		fakeroot \
		\
		sudo \
	&& apt-get build-dep -y linux

RUN useradd --comment 'LAARiD Development Account' \
		--home ${LAARID_HOME} --create-home \
		--shell /bin/bash \
		${LAARID_USER} \
	&& (echo "${LAARID_USER}:laarid" | chpasswd) \
	&& adduser ${LAARID_USER} sudo \
	&& (echo "${LAARID_USER} ALL=NOPASSWD: ALL" > /etc/sudoers.d/laarid) \
	&& chmod 0440 /etc/sudoers.d/laarid

VOLUME ["${LAARID_HOME}"]
WORKDIR ${LAARID_HOME}
USER ${LAARID_USER}
