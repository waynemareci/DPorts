# Created by: Mike McGaughey <mmcg@cs.monash.edu.au>
# $FreeBSD$

PORTNAME=	gc
PORTVERSION=	7.4.2
PORTREVISION=	2
CATEGORIES=	devel
MASTER_SITES=	http://www.hboehm.info/gc/gc_source/
PKGNAMEPREFIX=	boehm-
.ifdef GC_VARIANT
PKGNAMESUFFIX=	-${GC_VARIANT}
.endif

MAINTAINER=	cpm@fbsd.es
COMMENT=	Garbage collection and memory leak detection for C and C++

LICENSE=	BDWGC
LICENSE_NAME=	Boehm-Demers-Weiser Garbage Collector License
LICENSE_TEXT=	License can be found at http://www.hboehm.info/gc/license.txt
LICENSE_PERMS=	dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

BUILD_DEPENDS=	${LOCALBASE}/lib/libatomic_ops.a:${PORTSDIR}/devel/libatomic_ops

GNU_CONFIGURE=	yes
USES=		libtool pathfix pkgconfig
USE_LDCONFIG=	yes
INSTALL_TARGET=	install-strip
CONFIGURE_ARGS=	--enable-cplusplus --disable-static
MAKE_JOBS_UNSAFE=	yes

WRKSRC=		${WRKDIR}/${DISTNAME:C/[a-z]$//}

OPTIONS_DEFINE=	DEBUG

.ifdef GC_VARIANT
INSTLIBS=	cord gc gccpp
PLIST=		${NONEXISTENT}
PLIST_FILES=	${INSTLIBS:S,^,lib/lib,:S,$,-${GC_VARIANT}.so,} \
		${INSTLIBS:S,^,lib/lib,:S,$,-${GC_VARIANT}.so.1,} \
		${INSTLIBS:S,^,lib/lib,:S,$,-${GC_VARIANT}.so.1.0.3,} \
		libdata/pkgconfig/bdw-gc-${GC_VARIANT}.pc
RUN_DEPENDS+=	${LOCALBASE}/include/gc/gc.h:${PORTSDIR}/devel/boehm-gc
. if ${GC_VARIANT} == "redirect"
CONFIGURE_ARGS+=--disable-threads --enable-redirect-malloc
. endif
. if ${GC_VARIANT} == "threaded"
CONFIGURE_ARGS+=--enable-threads=posix --disable-redirect-malloc
OPTIONS_DEFINE+=PARALLEL_MARK
PARALLEL_MARK_DESC=	Parallel-thread marking (faster for SMP)
. endif
.else
CONFIGURE_ARGS+=--disable-threads --disable-redirect-malloc
OPTIONS_DEFINE+=DOCS
PORTDOCS=	*
.endif

NOT_FOR_ARCHS=	ia64

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MDEBUG}
CONFIGURE_ARGS+=--enable-gc-debug
PKGNAMESUFFIX:=	${PKGNAMESUFFIX}+fulldebug
.endif

.if defined(GC_VARIANT) && ${GC_VARIANT} == "threaded"
. if ${PORT_OPTIONS:MPARALLEL_MARK}
CONFIGURE_ARGS+=--enable-parallel-mark
. endif
.endif

.ifdef GC_VARIANT
post-patch:
	@${REINPLACE_CMD} -e \
		's,libgc\.la,libgc-${GC_VARIANT}.la,g ; \
		s,libgccpp\.la,libgccpp-${GC_VARIANT}.la,g ; \
		s,libcord\.la,libcord-${GC_VARIANT}.la,g' ${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} -e \
		's,-lgc,-lgc-${GC_VARIANT},' ${WRKSRC}/bdw-gc.pc.in

post-install:
	${RM} -r ${STAGEDIR}${PREFIX}/include
	${RM} -r ${STAGEDIR}${PREFIX}/share
	${MV} ${STAGEDIR}${PREFIX}/libdata/pkgconfig/bdw-gc.pc \
		${STAGEDIR}${PREFIX}/libdata/pkgconfig/bdw-gc-${GC_VARIANT}.pc

.else # ! GC_VARIANT

post-patch:
	@${REINPLACE_CMD} -e "s|%%PREFIX%%|${PREFIX}|g" ${WRKSRC}/doc/gc.man
	@${REINPLACE_CMD} \
		-e "s|(datadir)/@PACKAGE@|(datadir)/doc/@PACKAGE@|" \
		${WRKSRC}/Makefile.in

post-install:
	${INSTALL_MAN} ${WRKSRC}/doc/gc.man ${STAGEDIR}${MAN3PREFIX}/man/man3/gc.3
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	(cd ${WRKSRC}/doc && ${COPYTREE_SHARE} . ${STAGEDIR}${DOCSDIR})

.endif

regression-test: build
	(cd ${WRKSRC} && ${MAKE_CMD} check)

.include <bsd.port.mk>
