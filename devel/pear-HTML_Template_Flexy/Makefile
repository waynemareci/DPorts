# Created by: Antonio Carlos Venancio Junior (<antonio@inf.ufsc.br>)
# $FreeBSD$

PORTNAME=	HTML_Template_Flexy
PORTVERSION=	1.3.12
CATEGORIES=	devel www pear

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Extremely powerful Tokenizer driven Template engine

OPTIONS_DEFINE=	PEAR_HTML_JAVASCRIPT PEAR_FILE_GETTEXT PEAR_TRANSLATION2
PEAR_HTML_JAVASCRIPT_DESC=	PEAR::HTML_Javascript support
PEAR_FILE_GETTEXT_DESC=	PEAR::File_Gettext support
PEAR_TRANSLATION2_DESC=	PEAR::Translation2 support

USES=	pear

PEAR_HTML_JAVASCRIPT_RUN_DEPENDS=	${PEARDIR}/HTML/Javascript.php:${PORTSDIR}/devel/pear-HTML_Javascript
PEAR_FILE_GETTEXT_RUN_DEPENDS=	${PEARDIR}/File/Gettext.php:${PORTSDIR}/sysutils/pear-File_Gettext
PEAR_TRANSLATION2_RUN_DEPENDS=	${PEARDIR}/Translation2.php:${PORTSDIR}/sysutils/pear-Translation2

.include <bsd.port.mk>
