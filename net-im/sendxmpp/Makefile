# Created by: Max E. Kuznecov <mek@mek.uz.ua>
# $FreeBSD$

PORTNAME=	sendxmpp
PORTVERSION=	0.0.8
PORTREVISION=	2
CATEGORIES=	net-im perl5
MASTER_SITES=	http://www.djcbsoftware.nl/code/sendxmpp/

MAINTAINER=	mek@mek.uz.ua
COMMENT=	Perl-script to send xmpp (jabber) messages

RUN_DEPENDS+=	p5-Net-XMPP>0.0:${PORTSDIR}/net-im/p5-Net-XMPP \
		p5-IO-Socket-SSL>0.0:${PORTSDIR}/security/p5-IO-Socket-SSL

USES=		perl5
USE_PERL5=	configure

PLIST_FILES=	bin/sendxmpp man/man1/sendxmpp.1.gz

.include <bsd.port.mk>
