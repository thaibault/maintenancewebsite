#!/usr/bin/env bash
# -*- coding: utf-8 -*-
# region header
# Copyright Torben Sickert (info["~at~"]torben.website) 16.12.2012

# License
# -------

# This library written by Torben Sickert stand under a creative commons naming
# 3.0 unported license. see http://creativecommons.org/licenses/by/3.0/deed.de
# endregion
pkgname=legal-notes
pkgver=1.0.7
pkgrel=7
pkgdesc='Legal notes for documentation-, home- and websites.'
arch=('any')
license=('CC-BY-3.0')
depends=()
source=('index.html')
md5sums=('SKIP')
copyToAUR=true

package() {
    set +x
    pushd srcdir
    npm run build
    popd
    install -D --mode 755 "${srcdir}/index.compiled.html" \
        "${pkgdir}/usr/lib/legalNotes.html"
    set -x
}
# region vim modline
# vim: set tabstop=4 shiftwidth=4 expandtab:
# vim: foldmethod=marker foldmarker=region,endregion:
# endregion
