#!/usr/bin/env bash
# -*- coding: utf-8 -*-
# region header
# Copyright Torben Sickert (info["~at~"]torben.website) 16.12.2012

# License
# -------

# This library written by Torben Sickert stand under a creative commons naming
# 3.0 unported license. See https://creativecommons.org/licenses/by/3.0/deed.de
# endregion
pkgname=maintenance-website
pkgver=1.0.3
pkgrel=4
pkgdesc='Maintenance website for documentation-, home- and websites.'
arch=(any)
url=https://github.com/thaibault/maintenanceWebsite
license=(CC-BY-3.0)
depends=()
source=(index.html)
md5sums=(SKIP)
copy_to_aur=true

package() {
    set +x
    install -D --mode 755 "${srcdir}/index.html" \
        "${pkgdir}/usr/lib/maintenanceWebsite.html"
    set -x
}
# region vim modline
# vim: set tabstop=4 shiftwidth=4 expandtab:
# vim: foldmethod=marker foldmarker=region,endregion:
# endregion
