# Maintainer: Dāvis Mosāns <davispuh at gmail dot com>

pkgname=open-vm-tools-dkms
epoch=4
pkgver=9.4.6
_pkgsubver=1770165
pkgrel=3
pkgdesc='Open Virtual Machine Tools kernel modules (DKMS)'
arch=('i686' 'x86_64')
url='http://open-vm-tools.sourceforge.net/'
license=('GPL2')
conflicts=('open-vm-tools-modules', 'vmware-modules-dkms')

depends=('dkms')
options=('!strip')
optdepends=('open-vm-tools: Open Virtual Machine Tools'
            'linux-headers: Header files for Linux kernel')
install=open-vm-tools-dkms.install

_name='open-vm-tools'
_dirname='stable-9.4.x'
_version="${pkgver}-${_pkgsubver}"
_full_name="${_name}-${_version}"

source=(http://downloads.sourceforge.net/${_name}/${_full_name}.tar.gz
        0001-Remove-unused-DEPRECATED-macro.patch
        0002-Conditionally-define-g_info-macro.patch
        0003-Add-kuid_t-kgid_t-compatibility-layer.patch
        0004-Use-new-link-helpers.patch
        0005-Update-hgfs-file-operations-for-newer-kernels.patch
        0006-Fix-vmxnet-module-on-kernels-3.16.patch
        0007-Fix-vmhgfs-module-on-kernels-3.16.patch
        0008-Fix-segfault-in-vmhgfs.patch
        dkms.conf.in)
sha256sums=('54d7a83d8115124e4b809098b08d7017ba50828801c2f105cdadbc85a064a079'
            'a30ea0d0e2dd025eecb435c7a7b02b7c69e03fac8e67dc5d7f68998847a97240'
            '711e75244057b38de0b8523721106393de0fe9c2c82b0216c57c3b763b49798f'
            '1c685010a0e19456e71c60dd7d15550077da6ef37042d9df40d7e951611130aa'
            '91a46d4f7bc042b6d06e7a8cdf359f520ee95e9bf4d4bcaa3f11a701b388a40f'
            'e9b464790acbd429c6742a87b098ce51e7872511f75400d9d17afeaf2d2f6dea'
            'cbb7116499a33872e1861e050db81c3384e4ff59b767233d34b434ce12e899ad'
            'e8248176971056aca54d1e69a4b2f90e04a1589dd4b596b2af6746be9c3e96a3'
            '265a778624d72114f2afdc6619667fd116c4641bba6a42692acfb77a0f9bc81b'
            '5255a183cccd80b2bfbbf519b1cc8cec81ae40bbc0b5a88dfddd95532ece84ed')

prepare() {
  patch -d "$srcdir/${_full_name}" -Np2 -i "$srcdir/0001-Remove-unused-DEPRECATED-macro.patch"
  patch -d "$srcdir/${_full_name}" -Np2 -i "$srcdir/0002-Conditionally-define-g_info-macro.patch"
  patch -d "$srcdir/${_full_name}" -Np2 -i "$srcdir/0003-Add-kuid_t-kgid_t-compatibility-layer.patch"
  patch -d "$srcdir/${_full_name}" -Np2 -i "$srcdir/0004-Use-new-link-helpers.patch"
  patch -d "$srcdir/${_full_name}" -Np2 -i "$srcdir/0005-Update-hgfs-file-operations-for-newer-kernels.patch"
  patch -d "$srcdir/${_full_name}" -Np2 -i "$srcdir/0006-Fix-vmxnet-module-on-kernels-3.16.patch"
  patch -d "$srcdir/${_full_name}" -Np2 -i "$srcdir/0007-Fix-vmhgfs-module-on-kernels-3.16.patch"
  patch -d "$srcdir/${_full_name}" -Np2 -i "$srcdir/0008-Fix-segfault-in-vmhgfs.patch"
}

package() {
  cd "$srcdir/${_full_name}"
  sh ./modules/linux/dkms.sh ./ "${pkgdir}/usr/src"
  sed "s/%pkgver%/${pkgver}/g" "${srcdir}/dkms.conf.in" > "${pkgdir}/usr/src/${_name}-${pkgver}/dkms.conf"
  for _module in {"vmblock","vmci","vmsync","vsock"}; do
    rm -rf "${pkgdir}/usr/src/${_name}-${pkgver}/${_module}"
  done
}

