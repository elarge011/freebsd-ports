# Created by: Andrey <gugu@zoo.rambler.ru>
# $FreeBSD$

PORTNAME=	Algorithm-FloodControl
PORTVERSION=	2.001000
PORTREVISION=	2
CATEGORIES=	devel perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	perl@FreeBSD.org
COMMENT=	Robot protection

BUILD_DEPENDS=	p5-Params-Validate>=0:devel/p5-Params-Validate \
		p5-Cache-FastMmap>=0:devel/p5-Cache-FastMmap \
		p5-Class-Accessor>=0:devel/p5-Class-Accessor
RUN_DEPENDS:=	${BUILD_DEPENDS}

USES=		perl5
USE_PERL5=	configure

.include <bsd.port.mk>
