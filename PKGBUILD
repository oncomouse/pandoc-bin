pkgname=pandoc-bin
pkgver=2.17.1.1
pkgrel=1
pkgdesc="Pandoc - executable only, without 750MB Haskell depends/makedepends"
url="http://pandoc.org"
license=("GPL")
arch=('x86_64')
conflicts=("pandoc")
provides=("pandoc")
replaces=('pandoc-static' 'pandoc-lite')
depends=()
optdepends=(
    'texlive-core: for pdf output'
)

source=(
    "$pkgname-bin-$pkgver.tar.gz::https://github.com/jgm/pandoc/releases/download/${pkgver}/pandoc-${pkgver}-linux-amd64.tar.gz"

    # The binary release doesn't have the datafiles, so we need to yoink those out of the source tarball, too.
    "$pkgname-source-$pkgver.tar.gz::https://github.com/jgm/pandoc/archive/${pkgver}.tar.gz"
)
sha256sums=(bce0609dfe196784fe0300fb6847a2a246391a5b98e0490e5f7eadb78afb0d74
df7c6c605d084252fc28687dffe63ca57dd04a463698d323924d3be2f1f5df32)

package() {
    cd "${srcdir}/pandoc-${pkgver}"

    # To avoid having to download over a gigabyte of haskell makedepends (400-ish for ghc, plus 750 in libs), we
    # just yoink the binary from static compiled binary distributed by pandoc:
    mkdir -p "${pkgdir}/usr/share/pandoc"
    cp -R bin share "${pkgdir}/usr"


    # We're still missing all the datafiles and so on. We get those from the source tarball...
    cp -R data "${pkgdir}/usr/share/pandoc/"
    cp COPYRIGHT MANUAL.txt "${pkgdir}/usr/share/pandoc/"

    # When pandoc stopped having templates as a submodule, they copied various github turds into their source
    # tree, so let's tidy that up...
    rm -Rf ${pkgdir}/usr/share/pandoc/data/templates/{.github,README.markdown}
}
