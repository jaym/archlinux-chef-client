pkgname=chef-client
pkgver=12.1.0~rc.0
pkgrel=1
pkgdesc="Chef Client"
arch=('x86_64')
url="https://chef.io"
license=('Apache')
depends=()
conflicts=( chef chef-solo chef-dk )
source=("http://opscode-omnibus-packages.s3.amazonaws.com/ubuntu/13.04/x86_64/chef_$pkgver-${pkgrel}_amd64.deb")
sha256sums=('dca602985837f207d959789b897b24d2d141c8cd778bf9c936964e148299df49')


package() {
  cd "$srcdir"
  bsdtar -xf data.tar.gz -C "$pkgdir"

  # cleanup .git folders, any idea why they are in the package?
  find $pkgdir -type d -name ".git" | xargs  rm -rf

  # link executables
  binaries="chef-apply chef-client chef-shell knife"

  mkdir -p $pkgdir/usr/bin

  for binary in $binaries; do
    ln -sf /opt/chef/bin/$binary $pkgdir/usr/bin/ || error_exit "Cannot link $binary to /usr/bin"
  done
}
