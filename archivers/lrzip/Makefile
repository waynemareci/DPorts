# Created by: Gea-Suan Lin <gslin@gslin.org>
# $FreeBSD$

PORTNAME=	lrzip
PORTVERSION=	0.616
PORTREVISION=	1
CATEGORIES=	archivers
MASTER_SITES=	http://ck.kolivas.org/apps/lrzip/ \
		http://files.gslin.org/Software/

MAINTAINER=	delphij@FreeBSD.org
COMMENT=	Long Range ZIP or Lzma RZIP

LICENSE=	GPLv2

BUILD_DEPENDS=	nasm>=0:${PORTSDIR}/devel/nasm
LIB_DEPENDS=	liblzo2.so:${PORTSDIR}/archivers/lzo2

CFLAGS+=	-I${LOCALBASE}/include
CONFIGURE_ARGS+=	--enable-asm
GNU_CONFIGURE=	yes
LDFLAGS+=	-L${LOCALBASE}/lib
USES=		tar:bzip2 gmake pathfix perl5 libtool shebangfix
SHEBANG_FILES=	${WRKSRC}/lrztar
USE_PERL5=	build
USE_LDCONFIG=	yes

.include <bsd.port.mk>
