# $NetBSD: Makefile,v 1.59 2020/08/17 20:19:22 leot Exp $
#

DISTNAME=	cachesaver-0.10.9
PKGNAME=	claws-mail-cachesaver-0.10.9
PKGREVISION=	45
CATEGORIES=	mail
MASTER_SITES=	http://claws-mail.org/downloads/plugins_obsolete/

MAINTAINER=	pkgsrc-users@NetBSD.org
COMMENT=	Saves Claws-Mail metadata every 60 seconds

DEPENDS+=	claws-mail-${CLAWS_VERSION}{,nb[0-9]*}:../../mail/claws-mail

.include "../../mk/bsd.prefs.mk"

GNU_CONFIGURE=	yes
USE_LIBTOOL=	yes
USE_TOOLS+=	pkg-config
USE_LANGUAGES+=	c

.include "../../mail/claws-mail/Makefile.vers"
.include "../../mail/claws-mail/buildlink3.mk"
.include "../../security/gnutls/buildlink3.mk"
.include "../../x11/gtk2/buildlink3.mk"
.include "../../devel/glib2/buildlink3.mk"
.include "../../mk/bsd.pkg.mk"
