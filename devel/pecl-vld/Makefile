# Created by: chinsan
# $FreeBSD$

PORTNAME=	vld
PORTVERSION=	0.12.0
CATEGORIES=	devel pear
MASTER_SITES=	http://pecl.php.net/get/
PKGNAMEPREFIX=	pecl-
EXTRACT_SUFX=	.tgz
DIST_SUBDIR=	PECL

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Dump the internal representation of PHP scripts

LICENSE=	BSD

USE_PHP=	yes
USE_PHPEXT=	yes
IGNORE_WITH_PHP=	56

CONFIGURE_ARGS=	--enable-vld

.include <bsd.port.mk>
