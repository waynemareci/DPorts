# Created by: MAtthew Seaman
# $FreeBSD$

PORTNAME=	pgespresso
PORTVERSION=	1.0
CATEGORIES=	databases

MAINTAINER=	matthew@FreeBSD.org
COMMENT=	Optional extension to Barman backup and recovery manager

LICENSE=	PostgreSQL

USE_GITHUB=	yes
GH_ACCOUNT=	2ndquadrant-it
GH_COMMIT=	5715bb9

USES=		gmake pgsql:9.2+
WANT_PGSQL=	server

PLIST_FILES=	lib/postgresql/pgespresso.so			\
		share/postgresql/extension/pgespresso--1.0.sql	\
		share/postgresql/extension/pgespresso.control

PORTDOCS=	README.asciidoc

INSTALL_TARGET=	install-strip
MAKE_ARGS=	INSTALL="${INSTALL} -c"

post-install:
	${MKDIR} ${STAGEDIR}${DOCSDIR}/
	${INSTALL_MAN} ${WRKSRC}/${PORTDOCS} ${STAGEDIR}${DOCSDIR}/

.include <bsd.port.mk>
