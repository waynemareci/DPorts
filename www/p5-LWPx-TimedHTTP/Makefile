# Created by: Sunpoet Po-Chuan Hsieh <sunpoet@FreeBSD.org>
# $FreeBSD$

PORTNAME=	LWPx-TimedHTTP
PORTVERSION=	1.8
PORTREVISION=	1
CATEGORIES=	www perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Time the different stages of an HTTP request

LICENSE=	ART10 GPLv1
LICENSE_COMB=	dual

BUILD_DEPENDS=	p5-HTTP-Daemon>=0:${PORTSDIR}/www/p5-HTTP-Daemon \
		p5-libwww>=6:${PORTSDIR}/www/p5-libwww
RUN_DEPENDS=	p5-libwww>=6:${PORTSDIR}/www/p5-libwww

USE_PERL5=	configure
USES=		perl5

.include <bsd.port.mk>
