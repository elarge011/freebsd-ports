# $FreeBSD$

PORTNAME=	glib
PORTVERSION=	0.13.1.1
CATEGORIES=	devel haskell

MAINTAINER=	haskell@FreeBSD.org
COMMENT=	Binding to the GLIB library for Gtk2Hs

LICENSE=	LGPL21

USES=		pkgconfig
USE_CABAL=	gtk2hs-buildtools text>=1.0.0.0 utf8-string>=0.2
USE_GNOME=	glib20

.include "${.CURDIR}/../../lang/ghc/bsd.cabal.mk"
.include <bsd.port.mk>
