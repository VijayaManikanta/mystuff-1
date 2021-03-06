# $OpenBSD: Makefile,v 1.12 2010/11/16 11:23:28 espie Exp $

COMMENT =	platform game featuring buggers equipped with weapons

V =		0.6.1
DISTNAME =	teeworlds-${V}-source
PKGNAME =	teeworlds-${V}
CATEGORIES =	games
WRKSRC =	${WRKDIR}/teeworlds-b177-r50edfd37-source
WRKDIST =	${WRKDIR}/teeworlds-b177-r50edfd37-source

MAINTAINER =	Jonathan Armani <armani@openbsd.org>
HOMEPAGE =	http://www.teeworlds.com/

BAM_VERSION =	0.4.0
BAM_WRKSRC =	${WRKSRC}/bam-${BAM_VERSION}
BAM_TARGET =	release

MASTER_SITES =	http://www.teeworlds.com/files/ \
		https://github.com/downloads/matricks/bam/
DISTFILES =	${DISTNAME}${EXTRACT_SUFX} bam-${BAM_VERSION}.zip

# GPLv2
PERMIT_PACKAGE_CDROM =	Yes
PERMIT_PACKAGE_FTP =	Yes
PERMIT_DISTFILES_CDROM =Yes
PERMIT_DISTFILES_FTP =	Yes

WANTLIB =	GL GLU SDL X11 c m pthread stdc++ z freetype
LIB_DEPENDS =	devel/sdl

MODULES =	lang/python

NO_REGRESS =	Yes

GAMEDIR =	${PREFIX}/share/teeworlds

SUBST_VARS =	CC CXX CFLAGS

post-extract:
	@mv ${WRKDIR}/bam-${BAM_VERSION} ${BAM_WRKSRC}

pre-configure:
	${SUBST_CMD}	${WRKSRC}/src/engine/shared/storage.cpp\
		${WRKSRC}/scripts/make_src.py \
		${WRKSRC}/scripts/font_installer.sh \
		${WRKSRC}/bam.lua \
		${BAM_WRKSRC}/src/node.h \
		${BAM_WRKSRC}/src/context.h \
		${BAM_WRKSRC}/make_unix.sh \
		${BAM_WRKSRC}/src/base.lua

# build bam executable - teeworlds own build system
pre-build:
	cd ${BAM_WRKSRC} && /bin/sh -v make_unix.sh

do-build:
	cd ${WRKSRC} && CC=${CC} ${BAM_WRKSRC}/bam -v ${BAM_TARGET}

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/teeworlds ${PREFIX}/bin
	${INSTALL_PROGRAM} ${WRKSRC}/teeworlds_srv ${PREFIX}/bin
	${INSTALL_DATA_DIR} ${GAMEDIR}
	cd ${WRKSRC}; tar cf - data | tar xf - -C ${GAMEDIR}

.include <bsd.port.mk>
