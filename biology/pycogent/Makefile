# Created by: Wen Heping <wenheping@gmail.com>
# $FreeBSD$

PORTNAME=	pycogent
PORTVERSION=	1.5.3
PORTREVISION=	3
CATEGORIES=	biology python
MASTER_SITES=	SF/${PORTNAME}/PyCogent/${PORTVERSION}
DISTNAME=	PyCogent-${PORTVERSION}
EXTRACT_SUFX=	.tgz

MAINTAINER=	wen@FreeBSD.org
COMMENT=	Toolkit for statistical analysis of biological sequences

LICENSE=	GPLv2

BUILD_DEPENDS=	${PYNUMPY} \
		${LOCALBASE}/bin/cython:${PORTSDIR}/lang/cython \
		${LOCALBASE}/bin/sphinx-build:${PORTSDIR}/textproc/py-sphinx \
		${PYTHON_PKGNAMEPREFIX}sqlalchemy06>=0.5:${PORTSDIR}/databases/py-sqlalchemy06
RUN_DEPENDS:=	${BUILD_DEPENDS}

USES=		python
USE_PYTHON=	distutils autoplist

.include <bsd.port.mk>
