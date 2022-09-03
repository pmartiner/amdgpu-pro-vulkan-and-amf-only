plain '       .---.`               `.---.'
plain '    `/syhhhyso-           -osyhhhys/`'
plain '   .syNMdhNNhss/``.---.``/sshNNhdMNys.'
plain '   +sdMh.`+MNsssssssssssssssNM+`.hMds+'
plain '   :syNNdhNNhssssssssssssssshNNhdNNys:'
plain '    /ssyhhhysssssssssssssssssyhhhyss/'
plain '    .ossssssssssssssssssssssssssssso.'
plain '   :sssssssssssssssssssssssssssssssss:'
plain '  /sssssssssssssssssssssssssssssssssss/'
plain ' :sssssssssssssoosssssssoosssssssssssss:'
plain ' osssssssssssssoosssssssoossssssssssssso'
plain ' osssssssssssyyyyhhhhhhhyyyyssssssssssso'
plain ' /yyyyyyhhdmmmmNNNNNNNNNNNmmmmdhhyyyyyy/'
plain '  smmmNNNNNNNNNNNNNNNNNNNNNNNNNNNNNmmms'
plain '   /dNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNd/'
plain '    `:sdNNNNNNNNNNNNNNNNNNNNNNNNNds:`'
plain '       `-+shdNNNNNNNNNNNNNNNdhs+-`'
plain '             `.-:///////:-.`'

pkgname=amdgpu-pro-vulkan-and-amf-only
pkgver=22.20.3
_amdver=22.20.3
_pkgveramd=22.20-1462318~22.04
_amfver=1.4.26-1462318~22.04
_drmver=1_2.4.110.50203-1462318~22.04
pkgrel=1
arch=('x86_64')
url='http://www.amd.com'
license=('custom:AMD')
makedepends=('wget')

DLAGENTS='https::/usr/bin/wget --referer https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux.aspx -N %u'

source=(https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/v/vulkan-amdgpu-pro/vulkan-amdgpu-pro_${_pkgveramd}_amd64.deb
        https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/v/vulkan-amdgpu-pro/vulkan-amdgpu-pro_${_pkgveramd}_i386.deb
		https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/a/amf-amdgpu-pro/amf-amdgpu-pro_${_amfver}_amd64.deb
		https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/main/libd/libdrm-amdgpu/libdrm-amdgpu-amdgpu${_drmver}_amd64.deb
		https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/main/libd/libdrm-amdgpu/libdrm-amdgpu-amdgpu${_drmver}_i386.deb
		https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/main/libd/libdrm-amdgpu/libdrm-amdgpu-radeon${_drmver}_amd64.deb
		https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/main/libd/libdrm-amdgpu/libdrm-amdgpu-radeon${_drmver}_i386.deb)
sha256sums=('d31975ec084ec2c934f372685a091d79cd713415e171c2b07749ff1ed51a192d'
            '0176761780eed3127031b9dfcbc11d97a7dad04dad84311fcaa9f36b2e88c6fe'
			'c9109b2e2e7a164587e45fd872c51822bd849622c1ec9521bd850c35a8496d3c'
			'1ba0cb736986ffb11a1364224b7b110acae1d1a0cbfe776251e460629b6347da'
			'd7d51289e1a2a11079a1af639d77b44a25a17583e9345f58920c73a6ae3a6432'
			'f29137a7130e6ec70893a2d804f1f243cd50a0d8027d146209d2f9aa00481aa3'
			'52c7eaf2e9ddc2e4c532102d9492353280e097aec9da13d38de39fe8189ed39c')

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
	extract_deb "${srcdir}"/libdrm-amdgpu-amdgpu${_drmver}_amd64.deb
	extract_deb "${srcdir}"/libdrm-amdgpu-amdgpu${_drmver}_i386.deb
	extract_deb "${srcdir}"/libdrm-amdgpu-radeon${_drmver}_amd64.deb
	extract_deb "${srcdir}"/libdrm-amdgpu-radeon${_drmver}_i386.deb
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
	msg2 "64-bit lib in /opt/amdgpu/libdrm/x86_64-linux-gnu"
	msg2 ""
	msg2 "32-bit lib in /opt/amdgpu/libdrm/lib32/i386-linux-gnu"
	msg2 ""
	msg2 "changelog and copyright in /usr/share/doc/amf-amdgpu-pro"
	msg2 ""
	msg2 "#################################################################"
}
sudo rm /usr/lib/libamfrt64.so.1
sudo ln -s /opt/amdgpu-pro/lib/x86_64-linux-gnu/libamfrt64.so.1.4.26 /usr/lib/libamfrt64.so.1
