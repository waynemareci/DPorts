# $FreeBSD$

PORTNAME=	glib2
PORTVERSION=	2.2.0
CATEGORIES=	devel rubygems
MASTER_SITES=	RG

MAINTAINER=	ruby@FreeBSD.org
COMMENT=	Ruby binding for GLib2

RUN_DEPENDS=	rubygem-pkg-config>=0:${PORTSDIR}/devel/rubygem-pkg-config
BROKEN=		builds forever on DF with new glib

USE_GNOME=	glib20
USE_RUBY=	yes
USE_RUBYGEMS=	yes
RUBYGEM_AUTOPLIST=	yes

.include <bsd.port.mk>
