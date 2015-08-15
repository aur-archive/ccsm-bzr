# Submitter: Nathan Hulse <nat.hulse@gmail.com>

pkgname=ccsm-bzr
pkgver=808
pkgrel=3
pkgdesc="CompizConfig Settings Manager in Python"
arch=('any')
url="https://launchpad.net/compiz-ccsm"
license=('GPL')
depends=('compizconfig-python-bzr' 'pygtk' 'desktop-file-utils' )
optdepends=('xorg-xprop: grab various window properties for use in window matching rules')
makedepends=('bzr' 'intltool')
provides=('ccsm')
conflicts=('ccsm')
install='ccsm-bzr.install'

_bzrtrunk=lp:compiz-ccsm
_bzrmod=compiz-ccsm

build() {
  cd "$srcdir"

  msg "Connecting to Launchpad..."
  if [[ -d "$_bzrmod" ]]; then
    cd "$_bzrmod" && bzr pull "$_bzrtrunk" -r "$pkgver"
  else
    bzr branch "$_bzrtrunk" "$_bzrmod" -q -r "$pkgver"
  fi
  msg "Bazaar checkout done or server timeout."

  rm -rf "$srcdir/$_bzrmod-build"
  msg "Creating build directory..."
  cp -r "$srcdir/$_bzrmod" "$srcdir/$_bzrmod-build"
  cd "$srcdir/$_bzrmod-build"
  
  python2 setup.py build --prefix="/usr"
}

package() {
  cd "$srcdir/$_bzrmod-build"
  python2 setup.py install --prefix="/usr" --root="$pkgdir"
}
