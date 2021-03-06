# Created by: Mauricio Herrera Cuadra <mauricio@arareko.net>
# $FreeBSD$

PORTNAME=	bioperl-run
PORTVERSION=	1.6.901
PORTREVISION=	1
CATEGORIES=	biology perl5
PKGNAMEPREFIX=	p5-

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Wrapper modules for common bioinformatics tools

LICENSE=	ART10 GPLv3
LICENSE_COMB=	dual

BUILD_DEPENDS=	p5-bioperl>=1.6.0:${PORTSDIR}/biology/p5-bioperl \
		p5-IPC-Run>=0:${PORTSDIR}/devel/p5-IPC-Run \
		p5-Algorithm-Diff>=0:${PORTSDIR}/devel/p5-Algorithm-Diff \
		p5-XML-Twig>=0:${PORTSDIR}/textproc/p5-XML-Twig \
		p5-File-Sort>=0:${PORTSDIR}/misc/p5-File-Sort \
		p5-Config-Any>=0:${PORTSDIR}/devel/p5-Config-Any

RUN_DEPENDS:=	${BUILD_DEPENDS}

CONFLICTS=	p5-bioperl-run-1.[13579]*

USES=		perl5
USE_GITHUB=     yes
GH_ACCOUNT=     bioperl
GH_COMMIT=	96ccd93
GH_TAGNAME=     ${GH_COMMIT}

USES=		perl5 shebangfix
USE_PERL5=	modbuild
SHEBANG_FILES=	scripts/bioperl_application_installer.PLS \
		scripts/multi_hmmsearch.PLS \
		scripts/panalysis.PLS \
		scripts/papplmaker.PLS \
		scripts/run_neighbor.PLS \
		scripts/run_protdist.PLS \

OPTIONS_DEFINE=	DOCS

.include <bsd.port.options.mk>

post-build:
	cd ${WRKSRC} && ${PERL} ./Build manifest

post-install:
.for i in bioperl_application_installer multi_hmmsearch panalysis papplmaker run_neighbor run_protdist
	${CP} ${WRKSRC}/scripts/${i}.PLS ${STAGEDIR}${PREFIX}/bin/bp_${i}
.endfor
.if ${PORT_OPTIONS:MDOCS}
	${MKDIR} ${STAGEDIR}${DOCSDIR}
.for doc in AUTHORS Changes INSTALL.PROGRAMS README
	${INSTALL_DATA} ${WRKSRC}/${doc} ${STAGEDIR}${DOCSDIR}
.endfor
.endif

.include <bsd.port.mk>
