# $FreeBSD$

PORTNAME=	sdcc
PORTVERSION=	3.4.0
DISTVERSIONPREFIX=	src-
CATEGORIES=	lang
MASTER_SITES=	SF

MAINTAINER=	tijl@FreeBSD.org
COMMENT=	Small Device C Compiler

LICENSE=	GPLv3

BUILD_DEPENDS=	${LOCALBASE}/include/boost/graph/adjacency_list.hpp:${PORTSDIR}/devel/boost-libs

CONFLICTS_INSTALL=	sdcc-[0-9]* sdcc-devel-[0-9]*
GNU_CONFIGURE=	yes
USES=		gmake tar:bzip2

OPTIONS_DEFINE=		DEVLIB DOCS UCSIM
OPTIONS_MULTI=		TARGETS
OPTIONS_MULTI_TARGETS=	HC08 MCS51 PIC STM8 Z80
OPTIONS_DEFAULT=	DEVLIB UCSIM HC08 MCS51 PIC STM8 Z80
DEVLIB_DESC=	Device libraries
HC08_DESC=	Freescale 68HC08/S08
MCS51_DESC=	Intel MCS51, Maxim DS80C390/DS80C400
PIC_DESC=	Microchip PIC
UCSIM_DESC=	The ucSim simulator
STM8_DESC=	STMicroelectronics STM8
Z80_DESC=	Zilog Z80/Z180/GBZ80, Rabbit 2000/3000, Toshiba TLCS-90

CPPFLAGS+=	-idirafter ${LOCALBASE}/include
CONFIGURE_ARGS=	--disable-avr --disable-install-libbfd --disable-werror \
		--disable-st7 docdir=${DOCSDIR} sdcc_cv_c_fms_extensions=no
CONFIGURE_ENV=	ARCH=""
PORTDATA=	*
PORTDOCS=	*
WRKSRC=		${WRKDIR}/sdcc-${DISTVERSION}

OPTIONS_SUB=		yes
DEVLIB_CONFIGURE_OFF=	--disable-device-lib
HC08_CONFIGURE_OFF=	--disable-hc08 --disable-hc08-port		\
			--disable-s08-port
MCS51_CONFIGURE_OFF=	--disable-51 --disable-mcs51-port		\
			--disable-ds390-port --disable-ds400-port
PIC_BUILD_DEPENDS=	gputils>=1.2.0:${PORTSDIR}/devel/gputils
PIC_RUN_DEPENDS=	gpasm:${PORTSDIR}/devel/gputils
PIC_CONFIGURE_OFF=	--disable-pic14-port --disable-pic16-port
UCSIM_CONFIGURE_OFF=	--disable-ucsim
STM8_CONFIGURE_OFF=	--disable-stm8 --disable-stm8-port
Z80_CONFIGURE_OFF=	--disable-z80 --disable-z80-port		\
			--disable-z180-port --disable-gbz80-port	\
			--disable-r2k-port --disable-r3ka-port		\
			--disable-tlcs90-port

.include <bsd.port.options.mk>

.if ${ARCH} == "x86_64"
CONFIGURE_TARGET=	x86_64-portbld-freebsd${OSREL}
.endif

post-patch:
	@${REINPLACE_CMD} '/install:/s/:.*/:/' \
		${WRKSRC}/Makefile.in \
		${WRKSRC}/support/sdbinutils/libiberty/Makefile.in
.if ! ${PORT_OPTIONS:MDOCS}
	@${REINPLACE_CMD} 's, [a-z-]*doc,,' \
		${WRKSRC}/Makefile.in \
		${WRKSRC}/sim/ucsim/packages_in.mk
.endif

post-install:
	${FIND} -d ${STAGEDIR}${DATADIR} -type d -empty -delete

.include <bsd.port.mk>
