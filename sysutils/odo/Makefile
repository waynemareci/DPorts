# $FreeBSD$

PORTNAME=	odo
PORTVERSION=	0.2.2
CATEGORIES=	sysutils

MAINTAINER=	neel@neelc.org
COMMENT=	Atomic odometer for the command line

LICENSE=	ISCL

USE_GITHUB=	yes
GH_ACCOUNT=	atomicobject
GH_TAGNAME=	v${PORTVERSION}
GH_COMMIT=	a8160c9

PLIST_FILES=	bin/${PORTNAME} man/man1/${PORTNAME}.1.gz

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/man/${PORTNAME}.1 ${STAGEDIR}${MAN1PREFIX}/man/man1

regression-test: build
	cd ${WRKSRC} && ${SH} ./test_odo

.include <bsd.port.mk>
