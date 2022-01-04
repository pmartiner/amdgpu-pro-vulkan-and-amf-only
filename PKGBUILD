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
pkgver=21.40.2.1350683
_amdver=21.40.2
_pkgveramd=21.40.2-1350683
_amfver=1.4.23-1350683
pkgrel=1
arch=('x86_64')
url='http://www.amd.com'
license=('custom:AMD')
makedepends=('wget')

DLAGENTS='https::/usr/bin/wget --referer https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux.aspx -N %u'

source=(https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/v/vulkan-amdgpu-pro/vulkan-amdgpu-pro_${_pkgveramd}_amd64.deb
        https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/v/vulkan-amdgpu-pro/vulkan-amdgpu-pro_${_pkgveramd}_i386.deb
	https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/a/amf-amdgpu-pro/amf-amdgpu-pro_${_amfver}_amd64.deb)
sha256sums=('5e8e8387da1272f34f7bf9357609f473db2aad4c8d8ce19e3d803795abdc8133'
            '8213fc0829262c2d0299cf4f6d1412d092d0eeda5ef4714f0022a447d79e88f5'
	    '2181ad31c27c4fe086a04b32a94a40594bdfe15925a3e3ba58a64e44f9bbf359')

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

	sudo ln -s /opt/amdgpu-pro/lib/x86_64-linux-gnu/libamfrt64.so.1.4.23 /lib/libamfrt64.so.1	

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
}

