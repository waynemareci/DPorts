# Created by: Anders Nordby <anders@FreeBSD.org>
# $FreeBSD$

PORTNAME=	ffmpeg2theora
PORTVERSION=	0.29
PORTREVISION=	1
CATEGORIES=	multimedia
MASTER_SITES=	http://v2v.cc/~j/ffmpeg2theora/downloads/

MAINTAINER=	wg@FreeBSD.org
COMMENT=	Reencode many media file formats to Ogg Theora

LICENSE=	GPLv3

LIB_DEPENDS=	libavcodec.so:${PORTSDIR}/multimedia/ffmpeg \
		libkate.so:${PORTSDIR}/multimedia/libkate \
		libtheora.so:${PORTSDIR}/multimedia/libtheora

USES=		iconv pkgconfig scons tar:bzip2
MAKE_ENV=	APPEND_CCFLAGS="${CPPFLAGS}" APPEND_LINKFLAGS="${LDFLAGS}"

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

PLIST_FILES=	bin/ffmpeg2theora man/man1/ffmpeg2theora.1.gz

.include <bsd.port.mk>
