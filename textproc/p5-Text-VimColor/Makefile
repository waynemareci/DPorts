# Created by: Elvis Chiang <elvis@sslab.cs.ccu.edu.tw>
# $FreeBSD$

PORTNAME=	Text-VimColor
PORTVERSION=	0.14
PORTREVISION=	2
CATEGORIES=	textproc perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	ychsiao@ychsiao.org
COMMENT=	Syntax color text in HTML or XML using Vim

LICENSE=	ART10 GPLv1
LICENSE_COMB=	dual

BUILD_DEPENDS=	p5-File-ShareDir>=0:${PORTSDIR}/devel/p5-File-ShareDir \
		p5-File-ShareDir-Install>=0.03:${PORTSDIR}/devel/p5-File-ShareDir-Install \
		p5-Path-Class>=0:${PORTSDIR}/devel/p5-Path-Class \
		${LOCALBASE}/bin/vim:${PORTSDIR}/editors/vim
RUN_DEPENDS=	p5-File-ShareDir>=0:${PORTSDIR}/devel/p5-File-ShareDir \
		p5-Path-Class>=0:${PORTSDIR}/devel/p5-Path-Class \
		${LOCALBASE}/bin/vim:${PORTSDIR}/editors/vim

USES=		perl5
USE_PERL5=	configure

.include <bsd.port.mk>
