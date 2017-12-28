# Android boot.img tool
[![Build Status](https://travis-ci.org/cfig/Android_boot_image_editor.svg?branch=master)](https://travis-ci.org/cfig/Android_boot_image_editor)
[![License](http://img.shields.io/:license-apache-blue.svg?style=flat-square)](http://www.apache.org/licenses/LICENSE-2.0.html)

[中文快速说明](https://github.com/cfig/Android_boot_image_editor/blob/dev/short.md) 

This tool focuses on editing Android boot.img(also recovery.img and recovery-two-step.img).
It has been tested on Linux or Mac.

## Usage

### unpack

    cp <your_boot_image> boot.img
    ./gradew unpack

Your get the flattened kernel and /root under **build/unzip\_boot**:

    build/unzip_boot/
    ├── bootimg.json
    ├── kernel
    ├── second
    └── root

### pack

    ./gradew pack

The repacked file is **boot.img.signed**

#### If you are working with recovery.img
If you are working with recovery.img, the steps are similar:

    cp <original_recovery_image> recovery.img
    ./gradew unpack
    ./gradew pack

And you get recovery.img.signed

## Requirements

(1) Targeted boot.img MUST follows AOSP [verified boot flow](https://source.android.com/security/verifiedboot/index.html), which means it packs linux kernel, rootfs , and a optional second state bootloader, then sign it with OEM/USER keys.

(2) These utilities are known to work for Nexus (or Nexus compatible) boot.img for the following Android releases:

 - Lollipop (API Level 21,22) to Oreo (API Level 26,27)


## example & test
An example boot.img has been placed at **src/test/resources/boot.img**, which is extracted from Nexus 5x(code: bullhead) factory images from [Google](https://dl.google.com/dl/android/aosp/bullhead-mda89e-factory-29247942.tgz), you can take it as a quick start.

## boot.img layout
Read [layout](https://github.com/cfig/Android_boot_image_editor/blob/master/README.expert.md) of Android boot.img.
We now support **os\_version** and **os\_patch\_level**.

## References

boot\_signer
https://android.googlesource.com/platform/system/extras

bouncycastle
https://android.googlesource.com/platform/external/bouncycastle

cpio / fs\_config
https://android.googlesource.com/platform/system/core
