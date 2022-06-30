pkgname=amdgpu-pro-vulkan-and-amf-only
pkgver=22.20
pkgrel=1438747
_amdver=22.20
_pkgveramd=22.20-1438747~22.04
_amfver=1.4.26-1438747~22.04
arch=('x86_64')
url='http://www.amd.com'
license=('custom:AMD')
makedepends=('wget')

DLAGENTS='https::/usr/bin/wget --referer https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux.aspx -N %u'

source=(https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/v/vulkan-amdgpu-pro/vulkan-amdgpu-pro_${_pkgveramd}_amd64.deb
        https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/v/vulkan-amdgpu-pro/vulkan-amdgpu-pro_${_pkgveramd}_i386.deb
	https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/a/amf-amdgpu-pro/amf-amdgpu-pro_${_amfver}_amd64.deb)

sha256sums=('8030f2702805bf42192e34cb2d7beb647aec2afa2106e87229a047855d2429f7'
            '04145f457bc6e1491bc63485041926afb5b2b2290493d9dda9c026ab0c89d713'
            'b8a936bcb181ca02df12cbb67773442955834b5443e7a89618774c5771185c2a')

# extracts a debian package
# $1: deb file to extract
extract_deb() {
	local tmpdir="$(basename "${1%.deb}")"
	rm -Rf "$tmpdir"
	mkdir "$tmpdir"
	cd "$tmpdir"
	ar x "$1"
	tar -C "${pkgdir}" -xf data.tar.xz
}

package_amdgpu-pro-vulkan-and-amf-only () {
	pkgdesc="The AMDGPU Pro Vulkan and AMF drivers, without everything else"
	arch=('x86_64')

	extract_deb "${srcdir}"/vulkan-amdgpu-pro_${_pkgveramd}_amd64.deb
	extract_deb "${srcdir}"/vulkan-amdgpu-pro_${_pkgveramd}_i386.deb
	extract_deb "${srcdir}"/amf-amdgpu-pro_${_amfver}_amd64.deb
	
	rm -rf "${pkgdir}"/etc

	msg2 "#################################################################"
	msg2 ""
	msg2 "64-bit loader in /opt/amdgpu-pro/etc/vulkan/icd.d/amd_icd64.json"
	msg2 "32-bit loader in /opt/amdgpu-pro/etc/vulkan/icd.d/amd_icd32.json"
	msg2 ""
	msg2 "64-bit lib in /opt/amdgpu-pro/lib/x86_64-linux-gnu/amdvlk64.so"
	msg2 "32-bit lib in /opt/amdgpu-pro/lib/i386-linux-gnu/amdvlk32.so"
	msg2 ""
	msg2 "64-bit lib in /opt/amdgpu-pro/lib/x86_64-linux-gnu/libamfrt64.so"
	msg2 ""
	msg2 "changelog and copyright in /usr/share/doc/amf-amdgpu-pro"
	msg2 ""
	msg2 "#################################################################"
	sudo ln -sfn /opt/amdgpu-pro/lib/x86_64-linux-gnu/libamfrt64.so.1.4.24 /lib/libamfrt64.so.1
}
