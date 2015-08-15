# Maintainer: Sebastien Luttringer <seblu+arch@seblu.net>
# Contributor: Michal Soltys <soltys@ziu.info>

pkgname=ebtables
pkgver='2.0.10_2'
pkgrel=1
pkgdesc='Ethernet bridge filtering utilities'
arch=('i686' 'x86_64')
backup=('etc/conf.d/ebtables')
url='http://ebtables.sourceforge.net/'
license=('GPL2')
source=(
  "http://downloads.sourceforge.net/${pkgname}/${pkgname}-v${pkgver/_/-}.tar.gz"
  'ebtables.rc'
  'ebtables.conf'
  )
md5sums=('c5ae7fb75810fd936a5445239e853fd8'
         '368825c83a2b1180d2223e61b9f3bd07'
         '86fc3622e6fc0a7a7920c90ff576cc38')

build() {
  cd ${pkgname}-v${pkgver/_/-}
  make \
    CFLAGS='-Wunused -Wall -Werror -Wno-error=unused-but-set-variable' \
    LDFLAGS=''
}

package() {
  cd "${pkgname}-v${pkgver/_/-}"
  make install \
    DESTDIR="${pkgdir}" \
    LIBDIR=/usr/lib \
    MANDIR=/usr/share/man \
    BINDIR=/usr/sbin \
    INITDIR=/etc/rc.d \
    SYSCONFIGDIR=/etc/ebtables

  # rm package ebtables rc.d scripts
  rm "${pkgdir}/etc/rc.d/ebtables"
  rm "${pkgdir}/etc/ebtables/ebtables-config"

  # install custom ebtables rc.d scripts
  install -D -m 0755 "${srcdir}/ebtables.rc" "${pkgdir}/etc/rc.d/ebtables"
  install -D -m 0644 "${srcdir}/ebtables.conf" "${pkgdir}/etc/conf.d/ebtables"
}

# vim:set ts=2 sw=2 ft=sh et:
