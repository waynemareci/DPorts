# Created by: ijliao
# $FreeBSD$

PORTNAME=	speex
DISTVERSION=	1.2rc1
PORTREVISION=	7
PORTEPOCH=	1
CATEGORIES=	audio
MASTER_SITES=	http://downloads.us.xiph.org/releases/speex/

MAINTAINER=	multimedia@FreeBSD.org
COMMENT=	Open-source patent-free voice codec

LIB_DEPENDS=	libogg.so:${PORTSDIR}/audio/libogg

USES=		libtool:keepla pathfix
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-ogg-dir=${LOCALBASE}
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
INSTALL_TARGET=	install-strip

.include <bsd.port.pre.mk>

.if ${ARCH} == "i386" || ${ARCH} == "x86_64"
.if defined(MACHINE_CPU) && ${MACHINE_CPU:Msse}!=""
CONFIGURE_ARGS+=	--enable-sse
.endif
.endif

post-patch:
	@${FIND} ${WRKSRC} -name "Makefile.in" | ${XARGS} ${REINPLACE_CMD} -e \
		's|doc win32|win32|g ; \
		s|^mandir =.*$$|mandir = @mandir@|g'
	@${REINPLACE_CMD} -e 's|malloc.h|stdlib.h|' \
		${WRKSRC}/*/*.h
	@${REINPLACE_CMD} -e 's| in -lgnugetopt||g ; \
		 s|LIBS="-lgnugetopt|LIBS="|g' ${WRKSRC}/configure

.include <bsd.port.post.mk>
