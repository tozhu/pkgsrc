# $NetBSD: Makefile,v 1.33 2020/12/11 08:47:35 jaapb Exp $
#

GITHUB_PROJECT=	eliom
DISTNAME=	${GITHUB_PROJECT}-6.12.4
CATEGORIES=	www
MASTER_SITES=	${MASTER_SITE_GITHUB:=ocsigen/}

MAINTAINER=	jaapb@NetBSD.org
HOMEPAGE=	http://ocsigen.org/download/
COMMENT=	Dynamic webpage generation library
LICENSE=	gnu-lgpl-v2.1

USE_TOOLS+=		gmake
USE_LANGUAGES=		c
OCAML_USE_FINDLIB=	yes
UNLIMIT_RESOURCES+=	stacksize

DEPENDS+=	ocsigen>=2.16.1:../../www/ocsigen

.include "../../mk/ocaml.mk"

.if ${OCAML_USE_OPT_COMPILER} == "yes"
BUILD_TARGET=	all
.else
BUILD_TARGET=	byte
.endif

do-install:
	cd ${WRKSRC} && opam-installer --install --prefix ${DESTDIR}${PREFIX} --libdir ${DESTDIR}${PREFIX}/${OCAML_SITELIBDIR} --docdir ${DESTDIR}${PREFIX}/share/doc eliom.install

.include "../../devel/js_of_ocaml/buildlink3.mk"
.include "../../devel/ocaml-lwt_log/buildlink3.mk"
.include "../../devel/ocaml-lwt_ppx/buildlink3.mk"
.include "../../devel/ocaml-ppx_tools/buildlink3.mk"
.include "../../devel/ocaml-react/buildlink3.mk"
.include "../../devel/ocaml-reactiveData/buildlink3.mk"
.include "../../devel/ocamlbuild/buildlink3.mk"
.include "../../misc/ocaml-opam/buildlink3.mk"
BUILDLINK_DEPMETHOD.ocaml-opam?=    build
.include "../../net/ocaml-ipaddr/buildlink3.mk"
.include "../../net/ocamlnet/buildlink3.mk"
.include "../../security/ocaml-ssl/buildlink3.mk"
.include "../../textproc/ocaml-tyxml/buildlink3.mk"
.include "../../time/ocaml-calendar/buildlink3.mk"
.include "../../mk/bsd.pkg.mk"
