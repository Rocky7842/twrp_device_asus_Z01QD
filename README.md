TWRP device tree for Asus Zenfone 5z

The Asus Zenfone 5z (codenamed _"Z01R"_) are high-end smartphones from Asus.
Asus Zenfone 5z was announced and released in June 2018.

## Device specifications

| Baisc                   | Specification Sheet                                                                                                                 |
| ----------------------: | :---------------------------------------------------------------------------------------------------------------------------------- |
| SoC                     | Qualcomm SDM845 Snapdragon 845                                                                                                      |
| CPU                     | Octa-core (4x2.8 GHz Kryo 385 Gold & 4x1.8 GHz Kryo 385 Silver)                                                                     |
| GPU                     | Adreno 630                                                                                                                          |
| Memory                  | 4GB / 6GB / 8GB RAM (LPDDR4X)                                                                                                       |
| Shipped Android Version | 8.0 with ZenUI 5                                                                                                                    |
| Last version of Android | 10.0 with ZenUI 6                                                                                                                   |
| Storage                 | 64/128/256 GB UFS2.1                                                                                                                |
| Battery                 | Non-removable Li-Poly 3300 mAh battery                                                                                              |
| Display                 | 1080 x 2246 pixels, 18.7:9 ratio, 6.2 inches, IPS LCD (~402 ppi density)                                                            |
| Extras                  | Dual speakers, NFC                                                                                                                  |
| Rear Camera 1 (IMX363)  | 12MP, 4-axis OIS, f/1.8, 1/2.55" large sensor size, 1.4µm large pixel size, dual-pixel PDAF, 83° FOV, dual-LED (dual tone) flash    |
| Rear Camera 2 (ov8856)  | 8MP, f/2.0, 120° wide-angle camera                                                                                                  |
| Front Camera (ov8856)   | 8MP, 1.12µm, f/2.0, 84° FOV, 1080p 30 fps video                                                                                     |

## Device picture

![Asus Zenfone 5z](https://i.imgur.com/SL8yhBe.jpg)


## Kernel

Prebuilt kernel source:
https://github.com/5z-devs/android_kernel_asus_sdm845/commits/ffdc8c11296faba94bac36010a05b1f7e0ee5b35

## Compile

First repo init the twrp-12.1 tree:
```
mkdir ~/android/twrp-12.1
cd ~/android/twrp-12.1
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1
mkdir -p .repo/local_manifests
```

Then add to a local manifest (if you don't have .repo/local_manifest then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="osm0sis/twrp_abtemplate" path="bootable/recovery/installer" remote="github" revision="master"/>
  <project name="android_device_asus_Z01RD" path="device/asus/Z01RD" remote="TeamWin" revision="android-12.1"/>
</manifest>
```

Now you can sync your source:

```
repo sync
```

To automatically make the TWRP installer zip, you need to import this commit in the build/make path: https://gerrit.twrp.me/c/android_build/+/4964

Finally execute these:

```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch twrp_Z01RD-eng
make adbd bootimage
```
