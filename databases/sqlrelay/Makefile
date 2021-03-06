# Created by: Akinori MUSHA aka knu <knu@idaemons.org>
# $FreeBSD$

PORTNAME=	${SQLRELAY_PORTNAME}
PORTVERSION=	${SQLRELAY_PORTVERSION}
PORTREVISION=	1
CATEGORIES=	databases
MASTER_SITES=	SF

MAINTAINER=	pi@FreeBSD.org
COMMENT=	Persistent DB connection pooling/proxying/load balancing system

LIB_DEPENDS=	librudiments.so:${PORTSDIR}/devel/rudiments

WANT_GNOME=	yes
USES=		gmake libtool
CPPFLAGS+=	-I${LOCALBASE}/include
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=		${SQLRELAY_CONFIGURE_ARGS} \
			--disable-tcl \
			--disable-java \
			--disable-msql \
			--disable-perl \
			--disable-php \
			--disable-python \
			--disable-ruby \
			--disable-erlang \
			--disable-zope
MAKE_JOBS_UNSAFE=yes
USE_LDCONFIG=	yes

PORTDOCS=	*

TOSTRIP=	bin/sqlr-start \
		bin/sqlr-listener \
		bin/sqlr-connection \
		bin/sqlr-scaler \
		bin/sqlr-cachemanager \
		bin/sqlr-fields \
		bin/sqlr-query \
		bin/sqlr-export \
		bin/sqlr-import \
		bin/sqlr-pwdenc \
		bin/sqlr-status \
		bin/sqlrsh \
		lib/libsqlrutil.so.1.0.0 \
		lib/libsqlrclient.so.1.0.0 \
		lib/libsqlrclientwrapper.so.1.0.0 \
		lib/libpqsqlrelay.so.1.0.0 \
		lib/libmysql3sqlrelay.so.1.0.0 \
		lib/libmysql40sqlrelay.so.1.0.0 \
		lib/libmysql41sqlrelay.so.1.0.0 \
		lib/libmysql50sqlrelay.so.1.0.0 \
		lib/libmysql51sqlrelay.so.1.0.0 \
		lib/libsqlrserver.so.1.0.0 \
		libexec/sqlrelay/sqlrquery_sqlrcmdgstat.so \
		libexec/sqlrelay/sqlrquery_sqlrcmdcstat.so \
		libexec/sqlrelay/sqlrlogger_debug.so \
		libexec/sqlrelay/sqlrlogger_slowqueries.so \
		libexec/sqlrelay/sqlrlogger_custom_nw.so \
		libexec/sqlrelay/sqlrlogger_custom_sc.so \
		libexec/sqlrelay/sqlrpwdenc_rot.so \
		libexec/sqlrelay/sqlrpwdenc_md5.so \
		libexec/sqlrelay/sqlrpwdenc_crypt.so \
		libexec/sqlrelay/sqlrauth_default.so \
		libexec/sqlrelay/sqlrauth_sqlrelay.so \
		libexec/sqlrelay/sqlrconnection_router.so

.include "${.CURDIR}/Makefile.common"

OPTIONS_DEFINE=	MYSQL ODBC ORACLE PGSQL SQLITE3 FREETDS FIREBIRD DOCS
OPTIONS_SUB=	yes

ORACLE_CONFIGURE_ENABLE=	oracle

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MSQLITE3}
LIB_DEPENDS+=		libgdbm.so:${PORTSDIR}/databases/gdbm \
			libsqlite3.so:${PORTSDIR}/databases/sqlite3
CONFIGURE_ARGS+=	--with-gdbm-prefix="${LOCALBASE}" \
			--with-sqlite-prefix="${LOCALBASE}"
.else
CONFIGURE_ARGS+=	--without-gdbm-prefix \
			--disable-sqlite
.endif

.if ${PORT_OPTIONS:MMYSQL}
USE_MYSQL=	yes
CONFIGURE_ARGS+=	--with-mysql-prefix="${LOCALBASE}"
TOSTRIP+=		libexec/sqlrelay/sqlrconnection_mysql.so
.else
CONFIGURE_ARGS+=	--disable-mysql
.endif

.if ${PORT_OPTIONS:MFIREBIRD}
USE_FIREBIRD=	yes
CONFIGURE_ARGS+=	--with-firebird-prefix="${LOCALBASE}"
.else
CONFIGURE_ARGS+=	--disable-firebird
.endif

.if ${PORT_OPTIONS:MPGSQL}
USES+=			pgsql
CONFIGURE_ARGS+=	--with-postgresql-prefix="${LOCALBASE}"
.else
CONFIGURE_ARGS+=	--disable-postgresql
.endif

.if ${PORT_OPTIONS:MODBC}
LIB_DEPENDS+=		libodbc.so:${PORTSDIR}/databases/unixODBC
CONFIGURE_ARGS+=	--with-odbc-prefix="${LOCALBASE}"
.else
CONFIGURE_ARGS+=	--disable-odbc
.endif

.if ${PORT_OPTIONS:MFREETDS}
LIB_DEPENDS+=		libtds.so:${PORTSDIR}/databases/freetds
CONFIGURE_ARGS+=	--with-freetds-prefix="${LOCALBASE}"
.else
CONFIGURE_ARGS+=	--disable-freetds
.endif

post-patch:
	${REINPLACE_CMD} -E \
		-e 's,\$$\(initroot\),\$$\(initroot\)${PREFIX},g' \
		-e 's,/etc/rc.conf,/etc/defaults/rc.conf,g' \
			${WRKSRC}/init/Makefile
	@${REINPLACE_CMD} -e '/EXAMPLEDIR/d' ${WRKSRC}/etc/Makefile
	${FIND} ${WRKSRC} -name Makefile | ${XARGS} ${REINPLACE_CMD} -E \
		-e 's#-release \$$\(SQLR_VERSION\)##g;'

post-configure:
	@${REINPLACE_CMD} 's,-Werror,,' ${WRKSRC}/config.mk

post-stage:
.for f in ${TOSTRIP}
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/${f}
.endfor

.include <bsd.port.mk>
