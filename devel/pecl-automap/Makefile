# Created by: Ditesh Shashikant Gathani <ditesh@gathani.org>
# $FreeBSD$

PORTNAME=	automap
PORTVERSION=	2.1.0
CATEGORIES=	devel pear
MASTER_SITES=	http://pecl.php.net/get/
PKGNAMEPREFIX=	pecl-
EXTRACT_SUFX=	.tgz
DIST_SUBDIR=	PECL

MAINTAINER=	ports@FreeBSD.org
COMMENT=	PECL extension offering a fast map-based autoloader

LICENSE=	PHP301

USE_PHP=	spl
USE_PHP_BUILD=	yes
USE_PHPEXT=	yes
PHP_MODNAME=	automap
IGNORE_WITH_PHP=	56

CONFIGURE_ARGS=	--enable-automap

.include <bsd.port.mk>
