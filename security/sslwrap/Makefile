# Created by: Zahemszky, Gabor <ZGabor at CoDe dot HU>
# $FreeBSD$

PORTNAME=	sslwrap
PORTVERSION=	2.0.6
PORTREVISION=	1
CATEGORIES=	security
MASTER_SITES=	http://www.rickk.com/sslwrap/
DISTNAME=	${PORTNAME}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Another SSL Wrapper application, which uses SSLEay/OpenSSL

WRKSRC=		${WRKDIR}/${PORTNAME}${PORTVERSION:S/.//g}

USE_OPENSSL=	yes

PORTDOCS=	README docs.html
PLIST_FILES=	bin/sslwrap

OPTIONS_DEFINE=	DOCS

.include <bsd.port.options.mk>

post-patch:
	@${FIND} ${WRKSRC} -name "*.[ch]" | ${XARGS} ${REINPLACE_CMD} -e \
		's|SSL_OP_NON_EXPORT_FIRST|SSL_OP_CIPHER_SERVER_PREFERENCE|g ; \
		 s|OPENSSL"|"openssl/|g'

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/sslwrap ${STAGEDIR}${PREFIX}/bin
	${MKDIR} ${STAGEDIR}${DOCSDIR}
.for i in ${PORTDOCS}
	@${INSTALL_DATA} ${WRKSRC}/${i} ${STAGEDIR}${DOCSDIR}
.endfor

.include <bsd.port.mk>
