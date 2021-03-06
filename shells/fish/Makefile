# $NetBSD: Makefile,v 1.27 2020/12/04 20:45:40 nia Exp $

DISTNAME=		fish-3.1.2
PKGREVISION=		2
CATEGORIES=		shells
MASTER_SITES=		${MASTER_SITE_GITHUB:=fish-shell/}
GITHUB_PROJECT=		fish-shell
GITHUB_RELEASE=		${PKGVERSION_NOREV}

MAINTAINER=		pkgsrc-users@NetBSD.org
HOMEPAGE=		http://www.fishshell.com/
COMMENT=		User friendly command line shell for UNIX-like operating systems
LICENSE=		gnu-gpl-v2

USE_LANGUAGES+=		c c++03
USE_CMAKE=		yes
USE_TOOLS+=		msgfmt
CMAKE_ARGS+=		-DIntl_INCLUDE_DIR=${PREFIX}/include

PKG_SHELL=		bin/fish

REPLACE_PYTHON+=	share/tools/*.py
REPLACE_PYTHON+=	share/tools/web_config/webconfig.py

LDFLAGS.SunOS+=		-lintl

.include "../../mk/bsd.prefs.mk"

.if ${OPSYS} == "NetBSD" && exists(/usr/include/execinfo.h)
CPPFLAGS+=		-DHAVE_BACKTRACE
CPPFLAGS+=		-DHAVE_BACKTRACE_SYMBOLS
CXXFLAGS.NetBSD+=	-fpermissive
LDFLAGS+=		-lexecinfo
.endif

# Upstream intentionally omits open.1 on Darwin, but adds realpath.1
PLIST_VARS+=	open realpath
.if ${OPSYS} == "Darwin"
PLIST.realpath= yes
.else
PLIST.open=	yes
.endif

post-extract:
	${RM} ${WRKSRC}/version

.include "../../devel/pcre2/buildlink3.mk"
.include "../../devel/gettext-lib/buildlink3.mk"
.include "../../devel/gettext-tools/buildlink3.mk"
.if !empty(PKGSRC_COMPILER:M*gcc*)
.  include "../../devel/libatomic/buildlink3.mk"
.endif
.include "../../lang/python/application.mk"
.include "../../mk/curses.buildlink3.mk"
.include "../../mk/bsd.pkg.mk"
