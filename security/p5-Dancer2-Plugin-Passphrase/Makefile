# Created by: Henk van Oers <hvo.pm@xs4all.nl>
# $FreeBSD$

PORTNAME=	Dancer2-Plugin-Passphrase
PORTVERSION=	2.0.3
PORTREVISION=	1
CATEGORIES=	security perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	hvo.pm@xs4all.nl
COMMENT=	Passphrases and Passwords as objects for Dancer2

LICENSE=	ART10 GPLv1
LICENSE_COMB=	dual

BUILD_DEPENDS=	p5-Dancer2>=0.153002:${PORTSDIR}/www/p5-Dancer2 \
		p5-Data-Entropy>=0.005:${PORTSDIR}/security/p5-Data-Entropy \
		p5-Digest-Bcrypt>0:${PORTSDIR}/security/p5-Digest-Bcrypt \
		p5-Digest-SHA>=5.74:${PORTSDIR}/security/p5-Digest-SHA
RUN_DEPENDS:=	${BUILD_DEPENDS}

USES=		perl5
USE_PERL5=	configure

.include <bsd.port.mk>
