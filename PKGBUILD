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
pkgver=22.10.3
pkgrel=1420323 
_amdver=22.10.3
_pkgveramd=22.10.3-1420323
_amfver=1.4.24-1420323
arch=('x86_64')
url='http://www.amd.com'
license=('custom:AMD')
makedepends=('wget')

DLAGENTS='https::/usr/bin/wget --referer https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux.aspx -N %u'

source=(https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/v/vulkan-amdgpu-pro/vulkan-amdgpu-pro_${_pkgveramd}_amd64.deb
        https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/v/vulkan-amdgpu-pro/vulkan-amdgpu-pro_${_pkgveramd}_i386.deb
	https://repo.radeon.com/amdgpu/${_amdver}/ubuntu/pool/proprietary/a/amf-amdgpu-pro/amf-amdgpu-pro_${_amfver}_amd64.deb)
sha256sums=('6251e3f4003d305b60e6c82d4b01c933d23631b24f8d65081d5afa01f383dbe5'
            '4abd27433c147b52eb95787377b8a1f021007f5ca21d2f78d9798859420305b8'
            '872d2291dcdf4bc43e939b3b15ca02a490b75eb98e893c285b164ca49871e214')

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
