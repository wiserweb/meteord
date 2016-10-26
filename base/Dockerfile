FROM debian:jessie
MAINTAINER Jesse Rosenberger

ENV METEORD_DIR /opt/meteord
COPY scripts $METEORD_DIR

ARG NODE_VERSION
ENV NODE_VERSION ${NODE_VERSION:-4.6.1}
ONBUILD ENV NODE_VERSION ${NODE_VERSION:-4.6.1}

RUN bash $METEORD_DIR/lib/install_base.sh
RUN bash $METEORD_DIR/lib/install_node.sh
RUN bash $METEORD_DIR/lib/install_phantomjs.sh
RUN bash $METEORD_DIR/lib/cleanup.sh

RUN  apt-get update && apt-get -y dist-upgrade && echo "deb http://www.deb-multimedia.org jessie main" >> /etc/apt/sources.list && apt-get update && apt-get dist-upgrade &&  apt-get install -y --force-yes \
	deb-multimedia-keyring \
	graphicsmagick \
	graphicsmagick-imagemagick-compat \
	ffmpeg \
&& apt-get autoremove && apt-get clean \
&& rm -rf /var/lib/apt/lists/*

EXPOSE 80
ENTRYPOINT bash $METEORD_DIR/run_app.sh
