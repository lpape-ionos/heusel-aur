# Maintainer: Ariel AxionL <arielaxionl@gmail.com | axionl@aosc.io>
# Maintainer: Maarten de Boer <maarten@cloudstek.nl>
# Maintainer: Christian Heusel <christian@heusel.eu>
# Contributor: Johannes Pfrang <johannespfrang+arch @ gmail.com>
# Contributor: Emanuele 'Lele aka eldios' Calo' <xeldiosx@gmail.com>

_pkgname=teleport
pkgname=teleport-bin
pkgver=15.0.0
pkgrel=1
pkgdesc="Modern SSH server for teams managing distributed infrastructure"
arch=('i386' 'x86_64' 'armv7h' 'aarch64')
url="https://goteleport.com/"
license=('Apache')
provides=('teleport' 'tctl' 'tsh' 'tbot')
conflicts=('teleport')
install=teleport.install

source=("teleport.service"
        "teleport@.service"
        "teleport.install")

# The teleport servers do not allow for byte ranges to continue download so we set -C0
# https://aur.archlinux.org/packages/teleport-bin#comment-906339
DLAGENTS=('https::/usr/bin/curl -qgb "" -fL -C0 --retry 3 --retry-delay 3 -o %o %u')

source_i386=("teleport-bin-${pkgver}-i386.tar.gz::https://get.gravitational.com/teleport-v${pkgver}-linux-386-bin.tar.gz")
source_x86_64=("teleport-bin-${pkgver}-x86_64.tar.gz::https://get.gravitational.com/teleport-v${pkgver}-linux-amd64-bin.tar.gz")
source_armv7h=("teleport-bin-${pkgver}-armv7h.tar.gz::https://get.gravitational.com/teleport-v${pkgver}-linux-arm-bin.tar.gz")
source_aarch64=("teleport-bin-${pkgver}-aarch64.tar.gz::https://get.gravitational.com/teleport-v${pkgver}-linux-arm64-bin.tar.gz")

sha256sums=('22fd1ee136e9422458740811c9946de447105f26e87dbbc8daa35d17bd1f3894'
            '21ca4e56c9c5e1ce11570894e85ded853e26e91cc2e16ed9114b3d6a2c5c22ef'
            'ce2dd61cae3c0c3684e7e629f98b77551e66ddedca2194250a34f0efbc674f3a')
sha256sums_i386=('b8edad6f5d8ad6b6f5cce7a082920f1e8f140791b555dc79ef865c793c169461')
sha256sums_x86_64=('d90655f277aebcf481d88f8b18c33fbc9e356995df355e896991274a555500d0')
sha256sums_armv7h=('5c7f15b9d8561446d38f71354b5b0acf8af30baaadec4901c139bd4d324d307d')
sha256sums_aarch64=('d5588b1110b845d486baf6253ff5107a704122e0dabc2b52d9b1c8422ff56288')

options=(!strip)

package() {
    cd "${_pkgname}"

    # Install binaries
    install -Dm755 teleport "${pkgdir}/usr/bin/teleport"
    install -Dm755 tctl "${pkgdir}/usr/bin/tctl"
    install -Dm755 tsh "${pkgdir}/usr/bin/tsh"
    install -Dm755 tbot "${pkgdir}/usr/bin/tbot"

    # Install services
    install -Dm644 ${srcdir}/teleport.service "${pkgdir}/usr/lib/systemd/system/teleport.service"
    install -Dm644 ${srcdir}/teleport@.service "${pkgdir}/usr/lib/systemd/system/teleport@.service"

    # Copy example files
    install -dm755 "${pkgdir}/usr/share/teleport"
    cp -r examples "${pkgdir}/usr/share/teleport/"
}
