# Created by: steinex
# $FreeBSD$

PORTNAME=	Event-tcp
PORTVERSION=	0.14
PORTREVISION=	1
CATEGORIES=	net devel perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	5u623l20@gmail.com
COMMENT=	Glue code to build client-server style TCP-based services

LICENSE=	ART10 GPLv1
LICENSE_COMB=	dual

BUILD_DEPENDS=	p5-Event>=0:${PORTSDIR}/devel/p5-Event \
		p5-Ioctl>=0:${PORTSDIR}/devel/p5-Ioctl
RUN_DEPENDS:=	${BUILD_DEPENDS}

USES=		perl5
USE_PERL5=	configure

.include <bsd.port.mk>
