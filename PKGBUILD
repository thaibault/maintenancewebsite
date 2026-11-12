#!/usr/bin/env bash
# -*- coding: utf-8 -*-
# region header
# Copyright Torben Sickert (info["~at~"]tsickert.com) 16.12.2012

# License
# -------

# This library written by Torben Sickert stands under a creative commons naming
# 4.0 international license.
# See https://creativecommons.org/licenses/by/4.0/deed.de
# endregion
pkgname=maintenance-website
pkgver=1.0.5
pkgrel=1
pkgdesc='Maintenance website for documentation-, home- and websites.'
arch=(any)
url=https://github.com/thaibault/maintenancewebsite
license=(CC-BY-4.0)
depends=()
source=(index.html)
md5sums=(SKIP)
copy_to_aur=true

package() {
    set +x
    install -D --mode 644 "${srcdir}/index.html" \
        "${pkgdir}/usr/lib/maintenanceWebsite.html"
    set -x
}
