# Created by: Hye-Shik Chang <perky@FreeBSD.org>
# $FreeBSD$

PORTNAME=	eyed3
PORTVERSION=	0.6.18
PORTREVISION=	1
CATEGORIES=	audio python
MASTER_SITES=	http://eyed3.nicfit.net/releases/
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
PKGNAMESUFFIX=	-06
DISTNAME=	eyeD3-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Python module for processing ID3 tags

LICENSE=	GPLv2

USES=		gmake python:2
USE_PYTHON=	distutils autoplist
GNU_CONFIGURE=	yes

CONFLICTS=	py*-eyed3-0.7.[0-9]*

DOCSDIR=	${PREFIX}/share/doc/${PKGNAMEPREFIX}${PORTNAME}
PORTDOCS=	AUTHORS ChangeLog README
PLIST_FILES+=	bin/eyeD3 man/man1/eyeD3.1.gz

OPTIONS_DEFINE=	DOCS EXAMPLES

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}
	${INSTALL_MAN} ${WRKSRC}/doc/eyeD3.1 ${STAGEDIR}${MANPREFIX}/man/man1
	${INSTALL_SCRIPT} ${WRKSRC}/bin/eyeD3 ${STAGEDIR}${PREFIX}/bin

.include <bsd.port.mk>
