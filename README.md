# Only the vulkan and AMF parts of AMDGPU-PRO drivers

This is a fork of tkg's script for installing the Vulkan components of the AMDGPU-PRO drivers. I modified it so that it installs the AMF component as well. I modified tkg's script for my own personal use, but if you need to get AMF encoding working on an Arch based distro, then you can use this script to make things easier for you.

Can live next to RADV(but not AMDVLK, for some strange reason)

 https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux

Start your game/app with either:
- `VK_ICD_FILENAMES=/opt/amdgpu-pro/etc/vulkan/icd.d/amd_icd64.json` for 64-bit
or
- `VK_ICD_FILENAMES=/opt/amdgpu-pro/etc/vulkan/icd.d/amd_icd32.json` for 32-bit


You can also pass `VK_ICD_FILENAMES=/opt/amdgpu-pro/etc/vulkan/icd.d/amd_icd64.json:/opt/amdgpu-pro/etc/vulkan/icd.d/amd_icd32.json` if unsure. 

You need to run your app(e.g OBS) with the proprietary Vulkan drivers if you want to use AMF encoding.

## Build:
```
git clone https://github.com/DoomPenguin9/amdgpu-pro-vulkan-and-amf-only.git
cd amdgpu-pro-vulkan-and-amf-only
makepkg -si
```
