# Created by: Horia Racoviceanu <horia@racoviceanu.com>
# $FreeBSD$

PORTNAME=	galera
PORTVERSION?=	25.3.20
PORTREVISION?=	2
CATEGORIES=	databases

MAINTAINER=	devel@galeracluster.com
COMMENT=	Synchronous multi-master replication engine

LICENSE=	GPLv2

BUILD_DEPENDS=	checkmk:devel/check \
		${LOCALBASE}/include/boost/shared_ptr.hpp:devel/boost-libs
LIB_DEPENDS=	libboost_date_time.so:devel/boost-libs

BROKEN_aarch64=		fails to compile: gu_int128.h: use of undeclared identifier '__bswap64_var'
BROKEN_armv6=		fails to compile: gu_int128.h: use of undeclared identifier '__bswap64_var'
NOT_FOR_ARCHS=		i386
# On i386 older versions of clang produce:
#   cannot compile this atomic library call yet ... __atomic_add_fetch
# whereas newer ones generate a call to __atomic_add_fetch which ends up with
# undefined reference at link time:
#   undefined reference to `__atomic_fetch_add_8'
# https://bugs.llvm.org//show_bug.cgi?id=23262
# https://bugs.llvm.org//show_bug.cgi?id=24908
# https://tracker.crystax.net/issues/1263
NOT_FOR_ARCHS_REASON_i386=Uses 64 bit atomics that clang cannot generate on i386

USES=		execinfo python:build scons ssl

USE_LDCONFIG=	yes

USE_GITHUB=	yes
GH_ACCOUNT=	codership
GH_TAGNAME?=	release_${DISTVERSION}

LDFLAGS+=	-lboost_program_options -lboost_system
MAKE_ARGS+=	--config=force \
		deterministic_tests=1 \
		revno=${GH_TAGNAME} \
		system_asio=0

USE_RC_SUBR=	garb.sh

PLIST_FILES=	bin/garbd \
		lib/libgalera.so \
		lib/libgalera_smm.so

OPTIONS_DEFINE=	BOOSTPOOL BPOSTATIC DEBUG

BOOSTPOOL_DESC=	Use boost pool allocator
BPOSTATIC_DESC=	Use static boost_program_options

.include <bsd.port.pre.mk>

# COMPILER_TYPE could be empty on older FreeBSD versions.
.if "${COMPILER_TYPE}" == gcc || ${OSVERSION} < 1000000
USE_GCC=	4.8+
.endif

.if ${PORT_OPTIONS:MBOOSTPOOL}
MAKE_ARGS+=	boost_pool=1
.endif

.if ${PORT_OPTIONS:MBPOSTATIC}
MAKE_ARGS+=	bpostatic=${LOCALBASE}/lib/libboost_program_options.a
.endif

.if ${PORT_OPTIONS:MDEBUG}
MAKE_ARGS+=	debug=3
.endif

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/garb/garbd ${STAGEDIR}${PREFIX}/bin/
	${INSTALL_LIB} ${WRKSRC}/libgalera_smm.so ${STAGEDIR}${PREFIX}/lib/
	@(cd ${STAGEDIR}${PREFIX}/lib && ${LN} -sf libgalera_smm.so \
		libgalera.so)

.include <bsd.port.post.mk>
