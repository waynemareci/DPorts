# $FreeBSD$

PORTNAME=	git-extras
PORTVERSION=	2.2.0
CATEGORIES=	devel

MAINTAINER=	igor.ostapenko@gmail.com
COMMENT=	Sub-commands for repo summary, repl, changelog population, and more

LICENSE=	MIT

RUN_DEPENDS=	git:${PORTSDIR}/devel/git \
		bash:${PORTSDIR}/shells/bash

USE_GITHUB=	yes
GH_ACCOUNT=	tj
GH_COMMIT=	075d0ce

USES=		gmake shebangfix
SHEBANG_FILES=	bin/git-squash

NO_BUILD=	yes

.include <bsd.port.mk>
