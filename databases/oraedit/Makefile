# $NetBSD: Makefile,v 1.27 2020/12/04 20:45:04 nia Exp $

DISTNAME=	oraedit-0.1.4
PKGREVISION=	7
CATEGORIES=	databases
MASTER_SITES=	${MASTER_SITE_BACKUP}
EXTRACT_SUFX=	.tar.bz2

MAINTAINER=	pkgsrc-users@NetBSD.org
COMMENT=	Editor of PL/SQL source stored in Oracle database

NO_BUILD=	yes

REPLACE_PYTHON=		oraedit
INSTALLATION_DIRS=	bin

do-configure:;

do-install:
	${INSTALL_SCRIPT} ${WRKSRC}/oraedit ${DESTDIR}${PREFIX}/bin/oraedit

.include "../../lang/python/application.mk"
.include "../../mk/bsd.pkg.mk"
