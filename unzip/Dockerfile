FROM insideo/uc-linux:hydrogen
MAINTAINER ccondit@randomcoder.com

ADD control /control
RUN \
	mkdir -p /build /control /download /packages && \
	opkg update && \
	opkg install gcc make file linux-devel && \
	wget -O /download/unzip60.tar.gz \
		http://downloads.sourceforge.net/project/infozip/UnZip%206.x%20%28latest%29/UnZip%206.0/unzip60.tar.gz && \
	cd /build && \
	tar xf /download/unzip60.tar.gz && \
	cd unzip60 && \
	make -f unix/Makefile generic && \
	pre-root /build/unzip-root && \
	make -f unix/Makefile prefix=/build/unzip-root/usr install && \
	post-root /build/unzip-root && \
	cd /build/unzip-root && \
	rm -rf usr/man && \
	(strip --strip-unneeded usr/bin/* || true) && \
	mv usr/bin/unzipsfx usr/bin/unzipsfx.unzip && \
	mv usr/bin/unzip usr/bin/unzip.unzip && \
	mv usr/bin/zipgrep usr/bin/zipgrep.unzip && \
	mv usr/bin/funzip usr/bin/funzip.unzip && \
	rm usr/bin/zipinfo && \
	make-deb \
		/build/unzip-deb \
		/build/unzip-root \
		/control/unzip \
		/packages/unzip_6.0-1_amd64.deb

