# Created by: Giel van Schijndel <me@mortis.eu>
# $FreeBSD$

PORTNAME=	zfs-auto-snapshot
PORTVERSION=	1.1.0.1
PORTREVISION=	1
CATEGORIES=	sysutils

MAINTAINER=	me@mortis.eu
COMMENT=	ZFS Automatic Snapshot Service

USE_GITHUB=	yes
GH_ACCOUNT=	muggenhor
GH_COMMIT=	7b28bfe
GH_TAGNAME=	${GH_COMMIT}

NO_BUILD=	yes

MAN8_EN=	zfs-auto-snapshot.8
MANCOMPRESSED=	yes

PERIODIC_DIRS=	etc/periodic/frequent etc/periodic/hourly \
		etc/periodic/daily etc/periodic/weekly \
		etc/periodic/monthly etc/periodic

PERIODIC_FILES=	etc/periodic/frequent/000.${PORTNAME} \
               	etc/periodic/hourly/000.${PORTNAME} \
		etc/periodic/daily/000.${PORTNAME} \
		etc/periodic/weekly/000.${PORTNAME} \
		etc/periodic/monthly/000.${PORTNAME}

PLIST_FILES=	${PERIODIC_FILES} sbin/zfs-auto-snapshot ${MANPREFIX}/man/man8/zfs-auto-snapshot.8${MANEXT}
PLIST_DIRSTRY=	${PERIODIC_DIRS}

do-install:
	${INSTALL_SCRIPT} ${WRKSRC}/src/zfs-auto-snapshot.sh ${STAGEDIR}${PREFIX}/sbin/zfs-auto-snapshot
	${INSTALL_MAN} ${WRKSRC}/src/zfs-auto-snapshot.8 ${STAGEDIR}${MANPREFIX}/man/man8
.for _dir in ${PERIODIC_DIRS}
	@${MKDIR} ${STAGEDIR}${PREFIX}/${_dir}
.endfor

.for _file in ${PERIODIC_FILES}
	${SED} -e "s|/sbin/zfs-auto-snapshot|${PREFIX}/sbin/zfs-auto-snapshot|" \
		${WRKSRC}/${_file} > ${STAGEDIR}${PREFIX}/${_file}
	${CHMOD} ${BINMODE} ${STAGEDIR}${PREFIX}/${_file}
.endfor

.include <bsd.port.mk>
