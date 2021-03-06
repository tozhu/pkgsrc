# $NetBSD: Makefile,v 1.30 2020/04/26 09:47:39 rillig Exp $

DISTNAME=		binutils-2.30
PKGNAME=		${DISTNAME:S/^/avr-/}
CATEGORIES=		cross
MASTER_SITES=		${MASTER_SITE_GNU:=binutils/}
EXTRACT_SUFX=		.tar.bz2

MAINTAINER=		pkgsrc-users@NetBSD.org
COMMENT=		GNU binutils for Atmel AVR 8-bit RISC microcontrollers
LICENSE=		gnu-gpl-v3

# No need to use makeinfo - this package doesn't install the documentation.
USE_TOOLS+=		gmake
USE_LIBTOOL=		yes
GNU_CONFIGURE=		yes
GNU_CONFIGURE_STRICT=	no # several sub-configures know --enable-nls
USE_PKGLOCALEDIR=	yes
USE_GNU_CONFIGURE_HOST=	no

# follows to devel/binutils
# PR pkg/48504, ksh is sufficient for NetBSD 5.2 and NetBSD 6.1
.include "../../mk/bsd.prefs.mk"
.if !empty(MACHINE_PLATFORM:MNetBSD-[5-6].*-*) && \
	empty(MACHINE_PLATFORM:MNetBSD-6.99.*-*)
USE_TOOLS+=		ksh
CONFIG_SHELL=		ksh
.endif

CONFIGURE_ARGS+=	--disable-werror --target=avr --disable-nls

AUTO_MKDIRS=		yes

# Prevent the need to run texi2pod.pl and pod2man hence
# the need for perl as build dependency.
post-configure:
	set -e;							\
	cd ${WRKSRC};						\
	for f in ld/ldver.texi ld/ld.1 gas/doc/gasver.texi	\
	  gas/doc/as.1; do					\
		${TOUCH} $${f};					\
	done

# emulator/simulavr wants libbfd.so or libbfd.a and bfd.h
#  --with-bfd=path  location of AVR-binutils version of libbfd install
#  where include/bfd.h and lib/libbfd.a are found (from binutils)
post-build:
	set -e;							\
	(cd ${WRKSRC}/bfd; ${GMAKE} all libbfd.a);

post-install:
	# Emulator/simulvar needs library files
	(cd ${WRKSRC}/bfd; 					\
	${GMAKE} install-exec install-data; 			\
	${LIBTOOL} --mode install ${INSTALL_DATA} libbfd.la ${DESTDIR}${PREFIX}/avr/lib;	\
	${INSTALL_DATA} bfd.h ${DESTDIR}${PREFIX}/avr/include;	\
	)
	# emulator/simulavr wants following header files
	(cd ${WRKSRC}/include;					\
	for f in ansidecl.h symcat.h; do			\
	  ${INSTALL_DATA} $$f ${DESTDIR}${PREFIX}/avr/include;	\
	done;	\
	)
.include "../../mk/bsd.pkg.mk"
