# $FreeBSD$

PORTNAME=	tomsfastmath
PORTVERSION=	0.12
CATEGORIES=	math
MASTER_SITES=	http://libtom.org/files/
DISTNAME=	tfm-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Portable fixed precision math library for fast exponentiations

BROKEN_powerpc=	internal compiler error at src/mul/fp_mul_comba_48.c:398

USES=		gmake tar:bzip2
WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}
MAKEFILE=	makefile
ALL_TARGET=	default

PLIST_FILES=	include/tfm.h lib/libtfm.a

# Unbreak against Clang ("cc" is not a register)
post-patch:
	@${REINPLACE_CMD} -e 's,"%cc","cc",' \
		${WRKSRC}/src/mont/fp_montgomery_reduce.c \
		${WRKSRC}/src/mul/fp_mul_comba.c \
		${WRKSRC}/src/sqr/fp_sqr_comba.c

.include <bsd.port.mk>
