# $FreeBSD$

.include "Makefile.inc"

MULTILIB_LIST=	armv6-m,armv7-m,armv7e-m,armv7-r
PKGVERSION=	GNU Tools for ARM Embedded Processors

BUILD_PREFIX=	${WRKDIR}/build
DOC_PREFIX=	${INTERIM_PREFIX}/${DOCS_SUFFIX}

.if ${PORT_OPTIONS:MPURE}
WORLD_LIB=${INTERIM_WORLD}
.else
WORLD_LIB=${LOCALBASE}
.endif

.if ${PORT_OPTIONS:MSILENT}
LOG_PRE1=>
LOG_PREn=>>
LOG_POST=2>&1
.else
LOG_PRE1=2>&1 | tee
LOG_PREn=2>&1 | tee -a
LOG_POST=
.endif

LDFLAGS+=	-L${WORLD_LIB}/lib

.if ${CHOSEN_COMPILER_TYPE} == clang
CFLAGS+=	-Wno-error
CXXFLAGS+=	-Wno-error
.endif

MISC_DOCS=	license.txt readme.txt release.txt

.if ${PORT_OPTIONS:MPURE}
PREREQUISITES=		expat \
			zlib \
			libelf \
			gmp \
			mpfr \
			mpc \
			isl \
			cloog
ISL_CHECK_VERSION=
.else
PREREQUISITES=
ISL_CHECK_VERSION=	--disable-isl-version-check
.endif

ALL_BUILD=	build-binutils \
		build-gcc-first \
		build-newlib \
		build-newlib-nano \
		build-gcc-final \
		build-gcc-plugins \
		build-libstdcxx \
		build-gdb  \
		install-samples \
		install-misc \
		strip-binaries \
		strip-target-libraries

.PHONY: ${PREREQUISITES} ${ALL_BUILD}

all: ${PREREQUISITES} ${ALL_BUILD}

expat:
	@${ECHO_MSG} "====>  Build expat (log file: ${WRKDIR}/expat.log)"
	@${RM} -rf ${BUILD_PREFIX}/expat ${LOG_PRE1} ${WRKDIR}/expat.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/expat ${LOG_PREn} ${WRKDIR}/expat.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/expat && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/expat-${BUNDLED_VERSION_EXPAT}/configure \
	 --prefix=${INTERIM_WORLD} \
	 --disable-shared \
	 --disable-nls ${LOG_PREn} ${WRKDIR}/expat.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/expat all ${LOG_PREn} ${WRKDIR}/expat.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/expat install ${LOG_PREn} ${WRKDIR}/expat.log ${LOG_POST}

zlib:
	@${ECHO_MSG} "====>  Build zlib (log file: ${WRKDIR}/zlib.log)"
	@${RM} -rf ${BUILD_PREFIX}/zlib ${LOG_PRE1} ${WRKDIR}/zlib.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/zlib ${LOG_PREn} ${WRKDIR}/zlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Copy to build dir"
	@${TAR} -cf - -C ${SRC_DIR}/zlib-${BUNDLED_VERSION_ZLIB} . | ${TAR} -xf - -C ${BUILD_PREFIX}/zlib ${LOG_PREn} ${WRKDIR}/zlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Patch"
	@cd ${BUILD_PREFIX}/zlib && \
	 ${PATCH} -p1 < ${SRC_DIR}/zlib-${BUNDLED_VERSION_ZLIB}.patch ${LOG_PREn} ${WRKDIR}/zlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/zlib && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ./configure \
	 --static \
	 --prefix=${INTERIM_WORLD} ${LOG_PREn} ${WRKDIR}/zlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/zlib ${LOG_PREn} ${WRKDIR}/zlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/zlib install ${LOG_PREn} ${WRKDIR}/zlib.log ${LOG_POST}

libelf:
	@${ECHO_MSG} "====>  Build libelf (log file: ${WRKDIR}/libelf.log)"
	@${RM} -rf ${BUILD_PREFIX}/libelf ${LOG_PRE1} ${WRKDIR}/libelf.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/libelf ${LOG_PREn} ${WRKDIR}/libelf.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/libelf && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/libelf-${BUNDLED_VERSION_LIBELF}/configure \
	 --prefix=${INTERIM_WORLD} \
	 --disable-shared \
	 --disable-nls ${LOG_PREn} ${WRKDIR}/libelf.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/libelf all ${LOG_PREn} ${WRKDIR}/libelf.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/libelf install ${LOG_PREn} ${WRKDIR}/libelf.log ${LOG_POST}

gmp:
	@${ECHO_MSG} "====>  Build gmp (log file: ${WRKDIR}/gmp.log)"
	@${RM} -rf ${BUILD_PREFIX}/gmp ${LOG_PRE1} ${WRKDIR}/gmp.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/gmp ${LOG_PREn} ${WRKDIR}/gmp.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/gmp && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/gmp-${BUNDLED_VERSION_GMP}/configure \
	 --prefix=${INTERIM_WORLD} \
	 --enable-cxx \
	 --disable-shared \
	 --disable-nls ${LOG_PREn} ${WRKDIR}/gmp.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/gmp all ${LOG_PREn} ${WRKDIR}/gmp.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gmp install ${LOG_PREn} ${WRKDIR}/gmp.log ${LOG_POST}

mpfr:
	@${ECHO_MSG} "====>  Build mpfr (log file: ${WRKDIR}/mpfr.log)"
	@${RM} -rf ${BUILD_PREFIX}/mpfr ${LOG_PRE1} ${WRKDIR}/mpfr.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/mpfr ${LOG_PREn} ${WRKDIR}/mpfr.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/mpfr && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/mpfr-${BUNDLED_VERSION_MPFR}/configure \
	 --prefix=${INTERIM_WORLD} \
	 --with-gmp=${INTERIM_WORLD} \
	 --disable-shared \
	 --disable-nls ${LOG_PREn} ${WRKDIR}/mpfr.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/mpfr all ${LOG_PREn} ${WRKDIR}/mpfr.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/mpfr install ${LOG_PREn} ${WRKDIR}/mpfr.log ${LOG_POST}

mpc:
	@${ECHO_MSG} "====>  Build mpc (log file: ${WRKDIR}/mpc.log)"
	@${RM} -rf ${BUILD_PREFIX}/mpc ${LOG_PRE1} ${WRKDIR}/mpc.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/mpc ${LOG_PREn} ${WRKDIR}/mpc.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/mpc && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/mpc-${BUNDLED_VERSION_MPC}/configure \
	 --prefix=${INTERIM_WORLD} \
	 --with-gmp=${INTERIM_WORLD} \
	 --with-mpfr=${INTERIM_WORLD} \
	 --disable-shared \
	 --disable-nls ${LOG_PREn} ${WRKDIR}/mpc.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/mpc all ${LOG_PREn} ${WRKDIR}/mpc.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/mpc install ${LOG_PREn} ${WRKDIR}/mpc.log ${LOG_POST}

isl:
	@${ECHO_MSG} "====>  Build isl (log file: ${WRKDIR}/isl.log)"
	@${RM} -rf ${BUILD_PREFIX}/isl ${LOG_PRE1} ${WRKDIR}/isl.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/isl ${LOG_PREn} ${WRKDIR}/isl.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/isl && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/isl-${BUNDLED_VERSION_ISL}/configure \
	 --prefix=${INTERIM_WORLD} \
	 --with-gmp-prefix=${INTERIM_WORLD} \
	 --disable-shared \
	 --disable-nls ${LOG_PREn} ${WRKDIR}/isl.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/isl all ${LOG_PREn} ${WRKDIR}/isl.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/isl install ${LOG_PREn} ${WRKDIR}/isl.log ${LOG_POST}

cloog:
	@${ECHO_MSG} "====>  Build cloog (log file: ${WRKDIR}/cloog.log)"
	@${RM} -rf ${BUILD_PREFIX}/cloog ${LOG_PRE1} ${WRKDIR}/cloog.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/cloog ${LOG_PREn} ${WRKDIR}/cloog.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/cloog && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/cloog-${BUNDLED_VERSION_CLOOG}/configure \
	 --prefix=${INTERIM_WORLD} \
	 --with-bits=gmp \
	 --with-gmp-prefix=${INTERIM_WORLD} \
	 --with-isl-prefix=${INTERIM_WORLD} \
	 --disable-shared \
	 --disable-nls ${LOG_PREn} ${WRKDIR}/cloog.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/cloog all ${LOG_PREn} ${WRKDIR}/cloog.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/cloog install ${LOG_PREn} ${WRKDIR}/cloog.log ${LOG_POST}

build-binutils:
	@${ECHO_MSG} "====>  Build binutils (log file: ${WRKDIR}/binutils.log)"
	@${RM} -rf ${BUILD_PREFIX}/binutils ${LOG_PRE1} ${WRKDIR}/binutils.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/binutils ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/binutils && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/binutils/configure \
	 --target=${TARGET} \
	 --prefix=${INTERIM_PREFIX} \
	 --infodir=${DOC_PREFIX}/info \
	 --mandir=${DOC_PREFIX}/man \
	 --htmldir=${DOC_PREFIX}/html \
	 --pdfdir=${DOC_PREFIX}/pdf \
	 --disable-nls \
	 --enable-plugins \
	 --with-sysroot=${INTERIM_PREFIX}/${TARGET} \
	 --with-pkgversion="${PKGVERSION}" ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/binutils all ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/binutils install ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Prepare working area for library builds"
	@${MKDIR} ${BUILD_PREFIX}/target-libs ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
	@${TAR} -cf - -C ${INTERIM_PREFIX} . | ${TAR} -xf - -C ${BUILD_PREFIX}/target-libs ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
.if ${PORT_OPTIONS:MHTML} && ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} "=====>  Build HTML documentation"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/binutils html ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install HTML documentation into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/binutils install-html ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
.endif
.if ${PORT_OPTIONS:MPDF} && ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} "=====>  Build PDF documentation"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/binutils pdf ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install PDF documentation into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/binutils install-pdf ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}
.endif
	@${ECHO_MSG} "=====>  Cleanup installation"
	@${RM} -rf ${INTERIM_PREFIX}/lib ${LOG_PREn} ${WRKDIR}/binutils.log ${LOG_POST}

build-gcc-first:
	@${ECHO_MSG} "====>  Build preliminary gcc (log file: ${WRKDIR}/gcc-first.log)"
	@${RM} -rf ${BUILD_PREFIX}/gcc-first ${LOG_PRE1} ${WRKDIR}/gcc-first.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/gcc-first ${LOG_PREn} ${WRKDIR}/gcc-first.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/gcc-first && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/gcc/configure \
	 --target=${TARGET} \
	 --prefix=${INTERIM_PREFIX} \
	 --infodir=${DOC_PREFIX}/info \
	 --mandir=${DOC_PREFIX}/man \
	 --htmldir=${DOC_PREFIX}/html \
	 --pdfdir=${DOC_PREFIX}/pdf \
	 --libexecdir=${INTERIM_PREFIX}/lib \
	 --with-gmp=${WORLD_LIB} \
	 --with-mpfr=${WORLD_LIB} \
	 --with-mpc=${WORLD_LIB} \
	 --with-isl=${WORLD_LIB} \
	 ${ISL_CHECK_VERSION} \
	 --with-cloog=${WORLD_LIB} \
	 --with-libelf=${WORLD_LIB} \
	 --enable-languages=c \
	 --disable-decimal-float \
	 --disable-libffi \
	 --disable-libgomp \
	 --disable-libmudflap \
	 --disable-libquadmath \
	 --disable-libssp \
	 --disable-libstdcxx-pch \
	 --disable-nls \
	 --disable-shared \
	 --disable-threads \
	 --disable-tls \
	 --with-newlib \
	 --without-headers \
	 --with-gnu-as \
	 --with-gnu-ld \
	 --with-python-dir=share/gcc-${TARGET} \
	 --with-sysroot=${INTERIM_PREFIX}/${TARGET} \
	 --with-multilib-list=${MULTILIB_LIST} \
	 --with-pkgversion="${PKGVERSION}" ${LOG_PREn} ${WRKDIR}/gcc-first.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/gcc-first all ${LOG_PREn} ${WRKDIR}/gcc-first.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gcc-first install-gcc ${LOG_PREn} ${WRKDIR}/gcc-first.log ${LOG_POST}
	@${RM} -f ${INTERIM_PREFIX}/bin/${TARGET}-gccbug ${LOG_PREn} ${WRKDIR}/gcc-first.log ${LOG_POST}
	@${RM} -f ${INTERIM_PREFIX}/lib/libiberty.a ${LOG_PREn} ${WRKDIR}/gcc-first.log ${LOG_POST}
	@${RM} -rf ${INTERIM_PREFIX}/include ${LOG_PREn} ${WRKDIR}/gcc-first.log ${LOG_POST}

build-newlib:
	@${ECHO_MSG} "====>  Build newlib (log file: ${WRKDIR}/newlib.log)"
	@${RM} -rf ${BUILD_PREFIX}/newlib ${LOG_PRE1} ${WRKDIR}/newlib.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/newlib ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/newlib && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} PATH="${INTERIM_PREFIX}/bin:${PATH}" CFLAGS_FOR_TARGET="-g -O2 -ffunction-sections -fdata-sections" \
	  ${SRC_DIR}/newlib/configure \
	 --target=${TARGET} \
	 --prefix=${INTERIM_PREFIX} \
	 --infodir=${DOC_PREFIX}/info \
	 --mandir=${DOC_PREFIX}/man \
	 --htmldir=${DOC_PREFIX}/html \
	 --pdfdir=${DOC_PREFIX}/pdf \
	 --enable-newlib-io-long-long \
	 --enable-newlib-register-fini \
	 --disable-newlib-supplied-syscalls \
	 --disable-nls ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} PATH="${INTERIM_PREFIX}/bin:${PATH}" ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/newlib all ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into stage directory"
	@${MAKE_ENV} PATH="${INTERIM_PREFIX}/bin:${PATH}" ${MAKE_CMD} -C ${BUILD_PREFIX}/newlib install ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
.if ${PORT_OPTIONS:MHTML} && ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} "=====>  Build HTML documentation"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/newlib html ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install HTML documentation into stage directory"
	@${MKDIR} ${DOC_PREFIX}/html/libc ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@${TAR} -cf - -C ${BUILD_PREFIX}/newlib/${TARGET}/newlib/libc/libc.html . | ${TAR} -xf - -C ${DOC_PREFIX}/html/libc ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@${MKDIR} ${DOC_PREFIX}/html/libm ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@${TAR} -cf - -C ${BUILD_PREFIX}/newlib/${TARGET}/newlib/libm/libm.html . | ${TAR} -xf - -C ${DOC_PREFIX}/html/libm ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
.endif
.if ${PORT_OPTIONS:MPDF} && ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} "=====>  Build PDF documentation (ignore errors)"
	@-${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/newlib/${TARGET}/newlib/libc pdf ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@-${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/newlib/${TARGET}/newlib/libm pdf ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install PDF documentation into stage directory"
	@${CP} -f ${BUILD_PREFIX}/newlib/${TARGET}/newlib/libc/libc.pdf ${DOC_PREFIX}/pdf/libc.pdf ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
	@${CP} -f ${BUILD_PREFIX}/newlib/${TARGET}/newlib/libm/libm.pdf ${DOC_PREFIX}/pdf/libm.pdf ${LOG_PREn} ${WRKDIR}/newlib.log ${LOG_POST}
.endif

build-newlib-nano:
	@${ECHO_MSG} "====>  Build newlib-nano (log file: ${WRKDIR}/newlib-nano.log)"
	@${RM} -rf ${BUILD_PREFIX}/newlib-nano ${LOG_PRE1} ${WRKDIR}/newlib-nano.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/newlib-nano ${LOG_PREn} ${WRKDIR}/newlib-nano.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/newlib-nano && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} PATH="${INTERIM_PREFIX}/bin:${PATH}" CFLAGS_FOR_TARGET="-g -Os -ffunction-sections -fdata-sections" \
	  ${SRC_DIR}/newlib-nano-2.1/configure \
	 --target=${TARGET} \
	 --prefix=${BUILD_PREFIX}/target-libs \
	 --infodir=${DOC_PREFIX}/info \
	 --mandir=${DOC_PREFIX}/man \
	 --htmldir=${DOC_PREFIX}/html \
	 --pdfdir=${DOC_PREFIX}/pdf \
	 --disable-newlib-supplied-syscalls    \
	 --enable-newlib-reent-small           \
	 --disable-newlib-fvwrite-in-streamio  \
	 --disable-newlib-fseek-optimization   \
	 --disable-newlib-wide-orient          \
	 --enable-newlib-nano-malloc           \
	 --disable-newlib-unbuf-stream-opt     \
	 --enable-lite-exit                    \
	 --enable-newlib-global-atexit         \
	 --disable-nls ${LOG_PREn} ${WRKDIR}/newlib-nano.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} PATH="${INTERIM_PREFIX}/bin:${PATH}" ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/newlib-nano all ${LOG_PREn} ${WRKDIR}/newlib-nano.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} PATH="${INTERIM_PREFIX}/bin:${PATH}" ${MAKE_CMD} -C ${BUILD_PREFIX}/newlib-nano install  ${LOG_PREn} ${WRKDIR}/newlib-nano.log ${LOG_POST}

build-gcc-final:
	@${ECHO_MSG} "====>  Build final gcc and g++ (log file: ${WRKDIR}/gcc-final.log)"
	@${RM} -f ${INTERIM_PREFIX}/${TARGET}/usr ${LOG_PRE1} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${LN} -s . ${INTERIM_PREFIX}/${TARGET}/usr ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${RM} -rf ${BUILD_PREFIX}/gcc-final ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/gcc-final ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/gcc-final && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/gcc/configure \
	 --target=${TARGET} \
	 --prefix=${INTERIM_PREFIX} \
	 --infodir=${DOC_PREFIX}/info \
	 --mandir=${DOC_PREFIX}/man \
	 --htmldir=${DOC_PREFIX}/html \
	 --pdfdir=${DOC_PREFIX}/pdf \
	 --libexecdir=${INTERIM_PREFIX}/lib \
	 --with-gmp=${WORLD_LIB} \
	 --with-mpfr=${WORLD_LIB} \
	 --with-mpc=${WORLD_LIB} \
	 --with-isl=${WORLD_LIB} \
	 ${ISL_CHECK_VERSION} \
	 --with-cloog=${WORLD_LIB} \
	 --with-libelf=${WORLD_LIB} \
	 --enable-languages=c,c++ \
	 --enable-plugins \
	 --disable-decimal-float \
	 --disable-libffi \
	 --disable-libgomp \
	 --disable-libmudflap \
	 --disable-libquadmath \
	 --disable-libssp \
	 --disable-libstdcxx-pch \
	 --disable-nls \
	 --disable-shared \
	 --disable-threads \
	 --disable-tls \
	 --with-gnu-as \
	 --with-gnu-ld \
	 --with-newlib \
	 --with-headers=yes \
	 --with-python-dir=share/gcc-${TARGET} \
	 --with-sysroot=${INTERIM_PREFIX}/${TARGET} \
	 --with-multilib-list=${MULTILIB_LIST} \
	 --with-pkgversion="${PKGVERSION}" ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/gcc-final INHIBIT_LIBC_CFLAGS="-DUSE_TM_CLONE_REGISTRY=0" all ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gcc-final install ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
.if ${PORT_OPTIONS:MHTML} && ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} "=====>  Build HTML documentation"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gcc-final html ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install HTML documentation into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gcc-final install-html ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
.endif
.if ${PORT_OPTIONS:MPDF} && ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} "=====>  Build PDF documentation"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gcc-final pdf ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install PDF documentation into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gcc-final install-pdf ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
.endif
	@${ECHO_MSG} "=====>  Cleanup installation"
	@${RM} -f ${INTERIM_PREFIX}/bin/${TARGET}-gccbug ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${FIND} ${INTERIM_PREFIX}/${TARGET}/lib -name libiberty.a -delete ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${RM} -f ${INTERIM_PREFIX}/lib/libiberty.a ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${RM} -rf ${INTERIM_PREFIX}/include ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}
	@${RM} -f ${INTERIM_PREFIX}/${TARGET}/usr ${LOG_PREn} ${WRKDIR}/gcc-final.log ${LOG_POST}

build-gcc-plugins:
	@${ECHO_MSG} "====>  Build gcc plugins (log file: ${WRKDIR}/gcc-plugins.log)"
	@${RM} -f ${WRKDIR}/gcc-plugins.log
	@plugin_target_dir=$$(${INTERIM_PREFIX}/bin/${TARGET}-gcc -print-file-name=plugin) && \
	 plugins=$$(${FIND} ${SRC_DIR}/gcc-plugins -mindepth 1 -maxdepth 1 -type d -name '[^\.]*') && \
	 for plugin_dir in $${plugins} ; do \
	   plugin_name=$$(basename "$${plugin_dir}") && \
	   src_files=$$(${FIND} $${plugin_dir} -name \*.c -or -name \*.cc) && \
	   ${ECHO_MSG} "=====>  Build plugin $${plugin_name} from $${src_files}" && \
	   ${ECHO_MSG} "Build plugin $${plugin_name} from $${src_files}" >> ${WRKDIR}/gcc-plugins.log && \
	   ${CXX} ${CXXFLAGS} ${CPPFLAGS} -fPIC -fno-rtti -O2 -shared -I$${plugin_target_dir}/include -I${WORLD_LIB}/include $${src_files} \
	    -o $${plugin_target_dir}/$${plugin_name}.so ${LOG_PREn} ${WRKDIR}/gcc-plugins.log ${LOG_POST} ; \
	 done

build-libstdcxx:
	@${ECHO_MSG} "====>  Build size-optimized C++ runtime (log file: ${WRKDIR}/gcc-size-libstdcxx.log)"
	@${RM} -f ${BUILD_PREFIX}/target-libs/${TARGET}/usr ${LOG_PRE1} ${WRKDIR}/gcc-size-libstdcxx.log ${LOG_POST}
	@${LN} -s . ${BUILD_PREFIX}/target-libs/${TARGET}/usr ${LOG_PREn} ${WRKDIR}/gcc-size-libstdcxx.log ${LOG_POST}
	@${RM} -rf ${BUILD_PREFIX}/gcc-size-libstdcxx ${LOG_PREn} ${WRKDIR}/gcc-size-libstdcxx.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/gcc-size-libstdcxx ${LOG_PREn} ${WRKDIR}/gcc-size-libstdcxx.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/gcc-size-libstdcxx && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/gcc/configure \
	 --target=${TARGET} \
	 --prefix=${BUILD_PREFIX}/target-libs \
	 --infodir=${DOC_PREFIX}/info \
	 --mandir=${DOC_PREFIX}/man \
	 --htmldir=${DOC_PREFIX}/html \
	 --pdfdir=${DOC_PREFIX}/pdf \
	 --with-gmp=${WORLD_LIB} \
	 --with-mpfr=${WORLD_LIB} \
	 --with-mpc=${WORLD_LIB} \
	 --with-isl=${WORLD_LIB} \
	 ${ISL_CHECK_VERSION} \
	 --with-cloog=${WORLD_LIB} \
	 --with-libelf=${WORLD_LIB} \
	 --enable-languages=c,c++ \
	 --disable-decimal-float \
	 --disable-libffi \
	 --disable-libgomp \
	 --disable-libmudflap \
	 --disable-libquadmath \
	 --disable-libssp \
	 --disable-libstdcxx-pch \
	 --disable-nls \
	 --disable-shared \
	 --disable-threads \
	 --disable-tls \
	 --with-gnu-as \
	 --with-gnu-ld \
	 --with-newlib \
	 --with-headers=yes \
	 --with-python-dir=share/gcc-${TARGET} \
	 --with-sysroot=${BUILD_PREFIX}/target-libs/${TARGET} \
	 --with-multilib-list=${MULTILIB_LIST} \
	 --with-pkgversion="${PKGVERSION}" ${LOG_PREn} ${WRKDIR}/gcc-size-libstdcxx.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/gcc-size-libstdcxx \
	 CXXFLAGS_FOR_TARGET="-g -Os -ffunction-sections -fdata-sections -fno-exceptions" all ${LOG_PREn} ${WRKDIR}/gcc-size-libstdcxx.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into intermediate directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gcc-size-libstdcxx install ${LOG_PREn} ${WRKDIR}/gcc-size-libstdcxx.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Copy all target libraries into stage directory"
	@for multilib in $$(${BUILD_PREFIX}/target-libs/bin/${TARGET}-gcc -print-multi-lib) ; do \
	  multilib_dir=$${multilib%%;*} ; \
	  for srclib in libstdc++.a libsupc++.a libc.a libg.a librdimon.a nano.specs rdimon.specs nosys.specs ; do \
	    dstlib=$$(echo "$${srclib}" | ${SED} 's/\.a$$/_s.a/') ; \
	    ${CP} -f ${BUILD_PREFIX}/target-libs/${TARGET}/lib/$${multilib_dir}/$${srclib} ${INTERIM_PREFIX}/${TARGET}/lib/$${multilib_dir}/$${dstlib} ; \
	  done ; \
	  ${CP} -f ${BUILD_PREFIX}/target-libs/${TARGET}/lib/$${multilib_dir}/*crt0.o  ${INTERIM_PREFIX}/${TARGET}/lib/$${multilib_dir}/ ; \
	 done ${LOG_PREn} ${WRKDIR}/gcc-size-libstdcxx.log ${LOG_POST}

build-gdb:
	@${ECHO_MSG} "====>  Build gdb (log file: ${WRKDIR}/gdb.log)"
	@${RM} -rf ${BUILD_PREFIX}/gdb ${LOG_PRE1} ${WRKDIR}/gdb.log ${LOG_POST}
	@${MKDIR} ${BUILD_PREFIX}/gdb ${LOG_PREn} ${WRKDIR}/gdb.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Configure"
	@cd ${BUILD_PREFIX}/gdb && \
	 ${MAKE_ENV} ${CONFIGURE_ENV} ${SRC_DIR}/gdb/configure \
	 --target=${TARGET} \
	 --prefix=${INTERIM_PREFIX} \
	 --infodir=${DOC_PREFIX}/info \
	 --mandir=${DOC_PREFIX}/man \
	 --htmldir=${DOC_PREFIX}/html \
	 --pdfdir=${DOC_PREFIX}/pdf \
	 --disable-nls \
	 --disable-sim \
	 --with-libexpat \
	 --with-libexpat-prefix=${WORLD_LIB} \
	 --with-python=no \
	 --with-system-gdbinit=${INTERIM_PREFIX}/xxxx/${TARGET}/lib/gdbinit \
	 --with-lzma=no \
	 --with-gdb-datadir='$${prefix}/${TARGET}/share/gdb' \
	 --with-pkgversion="${PKGVERSION}" ${LOG_PREn} ${WRKDIR}/gdb.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Build"
	@${MAKE_ENV} ${MAKE_CMD} -j${MAKE_JOBS_NUMBER} -C ${BUILD_PREFIX}/gdb all ${LOG_PREn} ${WRKDIR}/gdb.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gdb install ${LOG_PREn} ${WRKDIR}/gdb.log ${LOG_POST}
	@${RM} -rf ${INTERIM_PREFIX}/include
.if ${PORT_OPTIONS:MHTML} && ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} "=====>  Build HTML documentation"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gdb html ${LOG_PREn} ${WRKDIR}/gdb.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install HTML documentation into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gdb install-html ${LOG_PREn} ${WRKDIR}/gdb.log ${LOG_POST}
.endif
.if ${PORT_OPTIONS:MPDF} && ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} "=====>  Build PDF documentation"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gdb pdf ${LOG_PREn} ${WRKDIR}/gdb.log ${LOG_POST}
	@${ECHO_MSG} "=====>  Install PDF documentation into stage directory"
	@${MAKE_ENV} ${MAKE_CMD} -C ${BUILD_PREFIX}/gdb install-pdf ${LOG_PREn} ${WRKDIR}/gdb.log ${LOG_POST}
.endif

install-samples:
.if ${PORT_OPTIONS:MEXAMPLES}
	@${ECHO_MSG} "====>  Install samples into stage directory"
	@${TAR} -xf ${SRC_DIR}/samples.tar.bz2 -C ${INTERIM_PREFIX}/share/gcc-${TARGET}
.else
	@${DO_NADA}
.endif

install-misc:
.if ${PORT_OPTIONS:MDOCS}
	@${ECHO_MSG} "====>  Install misc. files into stage directory"
	@for doc in ${MISC_DOCS} ; do \
	 ${CP} -f ${WRKDIR}/${ORIGINAL_PACKAGE_NAME}/$${doc} ${DOC_PREFIX}/ ; \
	 done
.else
	@${DO_NADA}
.endif

strip-binaries:
	@${ECHO_MSG} "====>  Strip host binaries"
	@for bin in $$(${FIND} ${INTERIM_PREFIX}/bin -type f -name ${TARGET}-\*) ; do \
	   if ! ${FILE} $$bin | ${GREP} -qs ': ELF' ; then continue ; fi ; \
	   ${STRIP_CMD} $${bin} ; \
	 done
	@for bin in $$(${FIND} ${INTERIM_PREFIX}/${TARGET}/bin -type f -maxdepth 1 -mindepth 1) ; do \
	   if ! ${FILE} $$bin | ${GREP} -qs ': ELF' ; then continue ; fi ; \
	   ${STRIP_CMD} $${bin} ; \
	 done
	@for bin in $$(${FIND} ${INTERIM_PREFIX}/lib/gcc/${TARGET}/4.8.4 -perm +111 -and ! -type d) ; do \
	   if ! ${FILE} $$bin | ${GREP} -qs ': ELF' ; then continue ; fi ; \
	   ${STRIP_CMD} $${bin} ; \
	 done

strip-target-libraries:
	@${ECHO_MSG} "====>  Strip target libraries"
	@for target in $$(${FIND} ${INTERIM_PREFIX}/${TARGET}/lib ${INTERIM_PREFIX}/lib/gcc/${TARGET}/4.8.4 -type f -name \*.a -o -name \*.o) ; do \
	   ${INTERIM_PREFIX}/bin/${TARGET}-objcopy -R .comment -R .note -R .debug_info -R .debug_aranges -R .debug_pubnames -R .debug_pubtypes -R .debug_abbrev -R .debug_line -R .debug_str -R .debug_ranges -R .debug_loc $${target} ; \
	done
	@${ECHO_MSG} "====>  Remove *.la files and other leftovers"
	@${FIND} ${INTERIM_PREFIX} -name \*.la -delete
	@${RM} -f ${INTERIM_PREFIX}/lib/charset.alias ${INTERIM_PREFIX}/lib/libiberty.a
