# $NetBSD: Makefile,v 1.25 2020/12/14 06:40:34 adam Exp $

DISTNAME=	msgpack-1.0.1
PKGNAME=	${PYPKGPREFIX}-${DISTNAME}
CATEGORIES=	devel python
MASTER_SITES=	${MASTER_SITE_PYPI:=m/msgpack/}

MAINTAINER=	pkgsrc-users@NetBSD.org
HOMEPAGE=	https://msgpack.org/
COMMENT=	MessagePack (de)serializer for Python
LICENSE=	apache-2.0

PYTHON_VERSIONED_DEPENDENCIES=	test:test

USE_LANGUAGES=	c c++

do-test:
	cd ${WRKSRC} && pytest-${PYVERSSUFFIX} test

.include "../../lang/python/egg.mk"
.include "../../lang/python/versioned_dependencies.mk"
.include "../../mk/bsd.pkg.mk"
