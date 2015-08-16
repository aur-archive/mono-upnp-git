# Maintainer: oke3 < Sekereg [at] gmx [dot] com >

pkgname=mono-upnp-git
pkgver=20120301
pkgrel=1
pkgdesc="A set of client/server libraries for the Universal Plug 'n Play specifications.'"
arch=('any')
url="http://www.mono-project.com"
license=('custom')
depends=('mono-addins' 'taglib-sharp' 'nunit-bzr')
makedepends=('git')
provides=('mono-upnp')
conflicts=('mono-upnp')

_gitroot=git://github.com/mono/mono-upnp.git
_gitname=mono-upnp

build() {
    cd "$srcdir"
    msg "Connecting to GIT server...."

    if [[ -d "$_gitname" ]]; then
        cd "$_gitname" && git pull origin && cd "$srcdir"
        msg "The local files are updated."
    else
        git clone "$_gitroot" "$_gitname"
    fi

    msg "GIT checkout done or server timeout"
    msg "Starting build..."

    rm -rf "$_gitname-build"
    git clone "$_gitname" "$_gitname-build"
    cd "$_gitname-build"

    ./autogen.sh
    ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var
    make
}

package() {
    cd "$srcdir/$_gitname-build"

    make DESTDIR="$pkgdir" install

    install -D -m644 COPYING $pkgdir/usr/share/licenses/$pkgname/COPYING
}
