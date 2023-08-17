## Variscite i.MX8 and i.MX8M High Assurance Boot

This layer includes support for signing imx-boot and Linux images for Variscite's i.MX8 family.

For more information, following these steps to find the i.MX8 HAB/AHAB guide for your Variscite System on Module and software release:

1. Visit https://variwiki.com/
2. Select a Variscite System on Module
3. Select "Developers Guide" under the Yocto software release
4. Select "Secure Boot / High Assurance Boot (HAB)"



## Prof of Concet NXP eval Kit  i.MX 8M Mini EVKB


```bash
repo init -u https://github.com/nxp-imx/imx-manifest -b imx-linux-mickledore -m imx-6.1.22-2.0.0.xml
repo sync

DISTRO=fsl-imx-wayland MACHINE=imx8mm-lpddr4-evk source imx-setup-release.sh -b build

# once you're set you can allways set environment using
# source setup-environment <build-dir>

# add this layer to conf/bblayers.conf

# enable hab in conf/local.conf 
# OVERRIDES =. "hab:"

# add patch 0001-add-HAB-tools.patch to "meta-imx"
# add patch 0001-WIC-use-signed-bootloader.patch to "meta-freescale"

# build
bitbake core-image-base

# flash
zstdcat core-image-base-imx8mm-lpddr4-evk.wic.zst | sudo dd of=/dev/sda bs=1M conv=fsync


```