FROM  --platform=$TARGETOS/$TARGETARCH oven/bun:latest

LABEL author="KhaoIsTheBest" maintainer="khao@khaodoes.dev"

RUN apt update \
            && apt -y install software-properties-common python3 python3-dev ffmpeg iproute2 git sqlite3 libsqlite3-dev ca-certificates dnsutils tzdata zip tar curl build-essential libtool tini net-tools iputils-ping \
            && useradd -m -d /home/container container

RUN chown -R container:container /bin/ping
RUN bun upgrade

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

STOPSIGNAL SIGINT

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT  ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]
