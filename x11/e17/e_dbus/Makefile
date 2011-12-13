# $OpenBSD: Makefile,v 1.9 2011/03/15 19:39:28 jasper Exp $

COMMENT =		EFL DBus component
DISTNAME =		e_dbus-1.1.0

SO_VERSION =		1.1
.for _lib in edbus enotify ehal eofono ebluez eukit
SHARED_LIBS +=		${_lib} ${SO_VERSION}
.endfor
SHARED_LIBS +=		econnman0_7x	2.0

# BSD
PERMIT_PACKAGE_CDROM =	Yes
PERMIT_PACKAGE_FTP =	Yes
PERMIT_DISTFILES_CDROM =Yes
PERMIT_DISTFILES_FTP =	Yes

USE_LIBTOOL =		Yes

WANTLIB += X11 X11-xcb c crypto dbus-1 ecore ecore_evas ecore_input 
WANTLIB += ecore_input_evas ecore_x eet eina evas expat fontconfig freetype 
WANTLIB += fribidi glib-2.0 jpeg m pcre pixman-1 pthread pthread-stubs ssl xcb 
WANTLIB += xcb-atom xcb-composite xcb-damage xcb-dpms xcb-event xcb-icccm 
WANTLIB += xcb-image xcb-keysyms xcb-property xcb-randr xcb-render 
WANTLIB += xcb-render-util xcb-screensaver xcb-shape xcb-shm xcb-sync 
WANTLIB += xcb-xfixes xcb-xinerama xcb-xprint xcb-xtest z

MODULES =		devel/gettext

LIB_DEPENDS =		x11/dbus \
			x11/e17/ecore>=1.1

CONFIGURE_ARGS =	--disable-doc

CONFIGURE_ENV +=	CFLAGS="${CFLAGS} -I${LOCALBASE}/include -Wall -Wextra" \
			LDFLAGS="${LDFLAGS} -L${LOCALBASE}/lib"

.include <bsd.port.mk>
