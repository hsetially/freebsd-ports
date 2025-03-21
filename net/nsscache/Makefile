PORTNAME=	nsscache
PORTVERSION=	0.49
PORTREVISION=	3
DISTVERSIONPREFIX=	version/
CATEGORIES=	net python

MAINTAINER=	kbowling@FreeBSD.org
COMMENT=	Python utility to create a local cache of directory services
WWW=		https://github.com/google/nsscache

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/COPYING

DEPRECATED=	Depends on expired devel/py-pytest-runner
EXPIRATION_DATE=2025-03-31

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pytest-runner>=0:devel/py-pytest-runner@${PY_FLAVOR}
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}boto3>0:www/py-boto3@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}python-ldap>0:net/py-python-ldap@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}packaging>0:devel/py-packaging@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pycurl>0:ftp/py-pycurl@${PY_FLAVOR}
TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}pytest-cov>0:devel/py-pytest-cov@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}pytest>0:devel/py-pytest@${PY_FLAVOR}

USES=		python
USE_GITHUB=	yes
GH_ACCOUNT=	google
USE_PYTHON=	autoplist distutils noflavors

NO_ARCH=	yes

PLIST_FILES=	'@dir /var/db/nsscache' \
		'@sample etc/nsscache.conf.sample' \
		share/man/man1/nsscache.1.gz \
		share/man/man5/nsscache.conf.5.gz

post-patch:
	@${REINPLACE_CMD} -e 's|/etc/nsscache.conf|${PREFIX}/etc/nsscache.conf|g' ${WRKSRC}/nss_cache/config.py
	@${REINPLACE_CMD} -e "s|%%PREFIX%%|${PREFIX}|g" ${WRKSRC}/nsscache.conf
	@${REINPLACE_CMD} -e "s|/var/lib/misc|/var/db/nsscache|g" ${WRKSRC}/nsscache.conf.5

post-install:
	${INSTALL_DATA} ${WRKSRC}/nsscache.conf ${STAGEDIR}${PREFIX}/etc/nsscache.conf.sample
	${INSTALL_MAN} ${WRKSRC}/nsscache.1 ${STAGEDIR}${PREFIX}/share/man/man1
	${INSTALL_MAN} ${WRKSRC}/nsscache.conf.5 ${STAGEDIR}${PREFIX}/share/man/man5
	@${MKDIR} ${STAGEDIR}/var/db/nsscache

do-test:
	cd ${WRKSRC} && ${PYTHON_CMD} setup.py test

.include <bsd.port.mk>
