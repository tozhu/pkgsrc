# $NetBSD: Makefile,v 1.14 2020/12/14 23:02:53 gutteridge Exp $

DISTNAME=	mozjs78_78.4.0.orig
PKGNAME=	${DISTNAME:S/_/-/:S/.orig//}
CATEGORIES=	lang
MASTER_SITES=	http://deb.debian.org/debian/pool/main/m/mozjs78/
EXTRACT_SUFX=	.tar.xz

MAINTAINER=	pkgsrc-users@NetBSD.org
HOMEPAGE=	https://mozilla-spidermonkey.github.io/
COMMENT=	SpiderMonkey JavaScript library (78.x branch)
LICENSE=	mpl-1.1

WRKSRC=		${WRKDIR}/firefox-${PKGVERSION_NOREV}
USE_TOOLS+=	autoconf213 gmake perl pkg-config
USE_LANGUAGES=	c c++

# "ERROR: Only GCC 7.1 or newer is supported"
GCC_REQD+=	7

CONFIGURE_DIRS=	js/src/build
BUILD_DIRS=	js/src/build

HAS_CONFIGURE=		yes
CONFIGURE_SCRIPT=	../configure
CONFIGURE_ARGS+=	--prefix=${PREFIX}
CONFIGURE_ARGS+=	--disable-debug
CONFIGURE_ARGS+=	--with-system-icu
CONFIGURE_ARGS+=	--with-system-zlib
CONFIGURE_ARGS+=	--enable-readline
CONFIGURE_ARGS+=	--disable-jemalloc
CONFIGURE_ARGS+=	--disable-debug-symbols
CONFIGURE_ARGS+=	--enable-strip
CONFIGURE_ARGS+=	--with-intl-api
# --disable-optimize
# For rustc/cargo detection
CONFIGURE_ARGS+=	--target=${MACHINE_GNU_PLATFORM}
CONFIGURE_ARGS+=	--host=${MACHINE_GNU_PLATFORM}

.include "../../mk/bsd.prefs.mk"

.if ${MACHINE_ARCH} == "i386"
# 64 bit atomics
CXXFLAGS+=		-march=i586
.endif

# XXX This does not work entirely correctly at present. There are
# 26 atomic type test failures on powerpc, where these pass on i386.
.if !empty(MACHINE_PLATFORM:MNetBSD-*-powerpc)
# 64 bit atomics
.include "../../devel/libatomic/buildlink3.mk"
.endif

SUBST_CLASSES+=		conf
SUBST_STAGE.conf=	pre-configure
SUBST_MESSAGE.conf=	Set variables in configuration file.
SUBST_FILES.conf+=	js/moz.configure
SUBST_VARS.conf=	PREFIX

PKGCONFIG_OVERRIDE+=	js/src/build/js.pc.in
PKGCONFIG_OVERRIDE+=	js/src/ctypes/libffi/libffi.pc.in

PYTHON_VERSIONS_INCOMPATIBLE=	27
PYTHON_FOR_BUILD_ONLY=		tool
TOOL_DEPENDS+=			${PYPKGPREFIX}-expat-[0-9]*:../../textproc/py-expat

TEST_DEPENDS+=			${PYPKGPREFIX}-six-[0-9]*:../../lang/py-six

TEST_TARGET=			check-jstests

pre-configure:
	cd ${WRKSRC}/js/src && \
	    autoconf-2.13 old-configure.in > old-configure && autoconf-2.13
	${MKDIR} ${WRKSRC}/js/src/build && \
	    ${TOUCH} ${WRKSRC}/js/src/build/old-configure.vars

post-install:
	cd ${DESTDIR}${PREFIX}/lib && \
		${MV} libmozjs-78.so libmozjs-78.so.0.0.0 && \
		${LN} -s libmozjs-78.so.0.0.0 libmozjs-78.so.0 && \
		${LN} -s libmozjs-78.so.0 libmozjs-78.so
	${RM} -f ${DESTDIR}${PREFIX}/lib/libjs_static.ajs
	${CHMOD} -x ${DESTDIR}${PREFIX}/include/mozjs-78/js-config.h
	${CHMOD} -x ${DESTDIR}${PREFIX}/lib/pkgconfig/mozjs-78.pc

BUILDLINK_DEPMETHOD.clang=	build
.include "../../lang/clang/buildlink3.mk"
RUST_REQ=	1.41.0
.include "../../lang/rust/rust.mk"
.include "../../devel/zlib/buildlink3.mk"
.include "../../lang/python/tool.mk"
.include "../../textproc/icu/buildlink3.mk"
.include "../../mk/readline.buildlink3.mk"
.include "../../mk/bsd.pkg.mk"
