#Maintainer chais[dot]z3r0[at]gmail[dot]com
pkgname=uplink-official
_pkgname=uplink
pkgver=1.55
pkgrel=1
pkgdesc="Trust is a weakness - a futuristic computer crime game. Requires official .deb package from the Introversion online store."
arch=('i686' 'x86_64')
_arch=i386
[ "$CARCH" = 'x86_64' ] && _arch=amd64
url="http://introversion.co.uk/uplink"
license=('custom')
depends=('mesa' 'libxdamage' 'freetype2')
[ "$CARCH" = 'x86_64' ] && depends=('mesa' 'lib32-libxdamage' 'lib32-freetype2')
provides=('uplink=1.55')
conflicts=('uplink' 'uplink-hib')
install='.install'
source=("uplink.desktop" "uplink.svg")
if [[ -e "${_pkgname}_${pkgver}-${pkgrel}_${_arch}.deb" ]]; then
	source=("${source[@]}" "${_pkgname}_${pkgver}-${pkgrel}_${_arch}.deb")
else
	echo "Game package not found in work directory. Please enter full path of the game package:"
	read _pkgpath
	source=("${source[@]}" "file://${_pkgpath}/${_pkgname}_${pkgver}-${pkgrel}_${_arch}.deb")
fi
sha256sums=('9bcaddbe9070985047891f22550c381d284d697fd0faec8fe8fe40eed165f8cf' '5d7b2b42f7f980812ab7a21bbcc4817601c5ce7010e4a5143f92c1c282983e9b')
[ "$CARCH" = 'i686' ] && sha256sums=("${sha256sums[@]}" "a86fb26e89addae51a6749f16e6a933ae588722c62c869ee93d494bdc29d07dc")
[ "$CARCH" = 'x86_64' ] && sha256sums=("${sha256sums[@]}" "07de90f21de7adb60996e963ad0a61becec04a992bc2c1ee870fade607f8c2ab")

build() {
	ar -vx "${srcdir}/${_pkgname}_${pkgver}-${pkgrel}_${_arch}.deb"
	tar -xzvf data.tar.gz
}

package() {
	for file in `ls ${srcdir}/usr/local/games/${_pkgname}/*dat`; do
		current=`basename $file`
		install -Dm644 "$file" "${pkgdir}/usr/local/games/${_pkgname}/${current}"
	done
	for file in `ls ${srcdir}/usr/local/games/${_pkgname}/*txt`; do
		current=`basename $file`
		install -Dm644 "$file" "${pkgdir}/usr/local/games/${_pkgname}/${current}"
	done
	for file in `ls ${srcdir}/usr/local/games/${_pkgname}/lib64/*`; do
		current=`basename $file`
		install -Dm644 "$file" "${pkgdir}/usr/local/games/${_pkgname}/lib64/${current}"
	done
	[ "$CARCH" = 'i686' ] && install -Dm755 ${srcdir}/usr/local/games/${_pkgname}/${_pkgname}.bin.x86 ${pkgdir}/usr/local/games/${_pkgname}/${_pkgname}.bin.x86
	[ "$CARCH" = 'x86_64' ] && install -Dm755 ${srcdir}/usr/local/games/${_pkgname}/${_pkgname}.bin.x86_64 ${pkgdir}/usr/local/games/${_pkgname}/${_pkgname}.bin.x86_64
	install -Dm644 ${srcdir}/uplink.svg ${pkgdir}/usr/local/games/${_pkgname}/uplink.svg
	install -d ${pkgdir}/usr/bin/
	[ "$CARCH" = 'i686' ] && ln -s "/usr/local/games/${_pkgname}/${_pkgname}.bin.x86" ${pkgdir}/usr/bin/uplink
	[ "$CARCH" = 'x86_64' ] && ln -s "/usr/local/games/${_pkgname}/${_pkgname}.bin.x86_64" ${pkgdir}/usr/bin/uplink
	install -Dm644 ${srcdir}/uplink.desktop ${pkgdir}/usr/share/applications/uplink.desktop
}
