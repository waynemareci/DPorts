# Created by: Ulrich Spoerlein <uspoerlein@gmail.com>
# $FreeBSD$

PORTNAME=	symon
PORTVERSION=	2.86
PORTREVISION=	2
CATEGORIES=	sysutils
MASTER_SITES=	http://wpd.home.xs4all.nl/symon/philes/ \
		${MASTER_SITE_LOCAL}
MASTER_SITE_SUBDIR=	uqs

MAINTAINER=	uqs@FreeBSD.org
COMMENT=	Performance and information monitoring tool

SUB_FILES=	pkg-message

USES=		perl5
USE_PERL5=	build
MAKE_JOBS_UNSAFE=	yes

USERS=		_symon
GROUPS=		_symon

# Synonym for WITHOUT_SYMUX
.if defined(WITHOUT_RRD)
WITHOUT_SYMUX=	yes
.endif

.if !defined(WITHOUT_SYMUX)
LIB_DEPENDS+=	librrd.so:${PORTSDIR}/databases/rrdtool
.endif

.if defined(WITHOUT_SYMUX) && defined(WITHOUT_SYMON)
IGNORE=	you have defined both WITHOUT_SYMUX or WITHOUT_RRD *and* WITHOUT_SYMON
.endif

SUBDIR=		lib
.if !defined(WITHOUT_SYMON)
SUBDIR+=	symon
PLIST_SUB+=	SYMON=""
USE_RC_SUBR+=	symon
.else
PLIST_SUB+=	SYMON="@comment "
.endif
.if !defined(WITHOUT_SYMUX)
SUBDIR+=	symux
PLIST_SUB+=	SYMUX=""
USE_RC_SUBR+=	symux
.else
PLIST_SUB+=	SYMUX="@comment "
.endif
SUBDIR+=	client

MAKE_ARGS+=	SUBDIR="${SUBDIR}" RRDDIR="${LOCALBASE}" \
		SYSCONFDIR="${PREFIX}/etc" PREFIX="${STAGEDIR}/${PREFIX}"

.include <bsd.port.pre.mk>

post-extract:
	@${MV} ${WRKDIR}/${PORTNAME} ${WRKSRC}

# We need to teach symon about mbstat changes/removal in r253351 and r253361.
post-patch:
	@${RM} ${WRKSRC}/platform/FreeBSD/sm_mbuf.c
	@${MKDIR} ${WRKSRC}/platform/DragonFly
	(cd ${WRKSRC}/platform && \
		 ${FIND} FreeBSD -type f \! -name sm_smart.c | \
		 ${XARGS} -n1 -I foo ${CP} foo DragonFly/)

.include <bsd.port.post.mk>
