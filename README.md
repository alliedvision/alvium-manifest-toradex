# Alvium CSI driver for Toradex systems

## Overview
This repository contains the manifest files for building the Allied Vision Alvium reference image for various Toradex systems.

## Compatibiliy
This release is tested with:
- Toradex Verdin iMX8M Plus SoM + Mallow carrier
- Alvium C series cameras with Firmware 14

The release is based on the Toradex BSP 7.1.0 and extendes the Toradex Yocto Reference Images. 
V4L2 and GenICam for CSI2 access is supported. Vimba X 2025-1 is required for GenICam for CSI2 access. 

## Quick Start
### Prerequisites
-  One of the supported board combinations: e.g Verdin iMX8M Plus + Mallow
-  Host PC: Install the requirements as defined in the [Yocto Project Reference Manual](https://docs.yoctoproject.org/5.0.7/ref-manual/system-requirements.html#required-packages-for-the-build-host)  
-  Alvium C series camera with Firmware 14

### Building the reference image

#### 1. Install required tools git-repo
```shell
mkdir -p ~/.bin
export PATH="${HOME}/.bin:${PATH}"
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo
chmod a+rx ~/.bin/repo
echo "export PATH=\"\${HOME}/.bin:\${PATH}\""  >> ~/.bashrc
```
#### 2. Create project directory 
```shell
mkdir -p avt-toradex-yocto
cd avt-toradex-yocto
```
#### 3. Install kas in project venv
```shell
python3 -m venv .venv
. ./.venv/bin/activte
python3 -m pip install kas
```
#### 4. Clone sources using repo
```shell
repo init https://github.com/alliedvision/alvium-manifest-toradex
repo sync
```
#### 5. Select a build configuration
The image is build using [kas](https://github.com/siemens/kas). For each board a kas configuration yaml file is available in the root directory after the checkout using repo. The following configuration files are currently available:
- verdin-imx8mp.yml: For Toradex Verdin iMX8M Plus systems 
#### 6. Accept NXP EULA
Some packages for the NXP SoCs require the NXP/Freescale EULA available in "toradex-bsp/layers/meta-freescale/EULA" to be read and accepted. To accept the license uncomment the following lines in the board configuration yaml file:
```yaml
#  accept-fsl-eula: |
#    ACCEPT_FSL_EULA = "1"  
```
#### 7. Build the AVT Image with the command:  
```shell
kas build <configuration .yml>
```
#### 8. Flash the image using the Toradex Easy Installer
Please follow the instructions from Toradex how to use the Toradex Easy Installer: [Flash a New Image Using Toradex Easy Installer](https://developer.toradex.com/easy-installer/toradex-easy-installer/flashing-new-image-using-tezi)
#### 9. Boot the board.
#### 10. Check if the camera firmware version is 14 or higher.
If the camera has an earlier firmware, perform an update with Vimba X Firmware Updater.

# Beta Disclaimer

Please be aware that all code revisions not explicitly listed in the Github Release section are
considered a **Beta Version**.

For Beta Versions, the following applies in addition to the BSD 3-Clause License:

THE SOFTWARE IS PRELIMINARY AND STILL IN TESTING AND VERIFICATION PHASE AND IS PROVIDED ON AN “AS
IS” AND “AS AVAILABLE” BASIS AND IS BELIEVED TO CONTAIN DEFECTS. THE PRIMARY PURPOSE OF THIS EARLY
ACCESS IS TO OBTAIN FEEDBACK ON PERFORMANCE AND THE IDENTIFICATION OF DEFECTS IN THE SOFTWARE,
HARDWARE AND DOCUMENTATION.