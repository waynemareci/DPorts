# Created by: Alex Dupre <ale@FreeBSD.org>
# $FreeBSD$

PORTNAME=	subversive
PORTVERSION=	2.0.0
PORTREVISION=	1
CATEGORIES=	devel java
MASTER_SITES=	${MASTER_SITE_ECLIPSE:S,%SUBDIR%,technology/subversive/2.0/builds,:S,$,:core,} \
		http://community.polarion.com/projects/subversive/download/eclipse/4.0/builds/:connectors
DISTNAME=	Subversive-${PORTVERSION}.I20140519-1700
DISTFILES=	${DISTNAME}${EXTRACT_SUFX}:core ${CONNECTORS}:connectors

MAINTAINER=	ale@FreeBSD.org
COMMENT=	Eclipse plug-in that provides Subversion support

LICENSE=	EPL

RUN_DEPENDS=	eclipse:${PORTSDIR}/java/eclipse

CONNECTORS=	Subversive-connectors-allplatforms-4.0.2.I20140528-1700.zip

USES=		zip
NO_WRKSUBDIR=	yes

.include "${.CURDIR}/../../java/eclipse/Makefile.plugins"

.include <bsd.port.mk>
