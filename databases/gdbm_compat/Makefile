# $NetBSD: Makefile,v 1.10 2020/08/24 07:59:26 wiz Exp $

.include "../../databases/gdbm/Makefile.common"

PKGNAME=	${DISTNAME:S/-/_compat-/}

COMMENT+=	Compat library for dbm and ndbm

DEPENDS+=	gdbm-${PKGVERSION_NOREV}{,nb[0-9]*}:../../databases/gdbm

CONFIGURE_ARGS+=	--enable-libgdbm-compat

BUILD_DIRS=		compat

post-extract:
	${LN} -s ${BUILDLINK_PREFIX.gdbm}/lib/libgdbm.la ${WRKSRC}/src

.include "../../databases/gdbm/buildlink3.mk"
.include "../../mk/bsd.pkg.mk"
