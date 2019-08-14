FROM alpine:latest
RUN apk update && apk add ca-certificates
# for self-signed CA
#COPY ./mycert.crt /usr/local/share/ca-certificates/mycert.crt
#RUN update-ca-certificates
# core user env
RUN apk add --virtual core-env \
	coreutils curl diffutils findutils gawk grep \
	make patch perl python2-dev tar unzip util-linux vim wget
# multi-user-env
RUN apk add --virtual user-env \
	bash shadow sudo
RUN apk add --virtual build-essential \
	asciidoc build-base bzip2 cdrkit flex \
	gcc g++ git gettext libxslt linux-headers \
	ncurses-dev zlib-dev
# create user
RUN useradd -m openwrt && \
	echo 'openwrt ALL=NOPASSWD: ALL' > /etc/sudoers.d/openwrt
USER openwrt
WORKDIR /home/openwrt
# get openwrt
#RUN git config --global http.proxy http://proxy:port
RUN git clone https://github.com/openwrt/openwrt.git -b openwrt-18.06 --depth=1 && \
	openwrt/scripts/feeds update -a
