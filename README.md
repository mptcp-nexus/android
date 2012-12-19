Android 4.1.2 with MPTCP
========================

This is a Multipath TCP port for Android 4.1.2. Currently, it runs only on Nexus S.

## Requirements
### Initialize build environment
See http://source.android.com/source/initializing.html

The following may take a while. You can speed up the syncing and building using the -jn option, which will separate the task up into n threads.
For building there are three different options:
##### The AOSP+MPTCP with Root Access (Google Apps are integrated automatically)
Run:

```
$repo init -u https://github.com/multipath-tcp/android.git -b root
$repo sync -j4
```
After synchronising the repo you need to run from the root directory of the repository:
  
```
$./script/enhanceAOSP -root
```
##### The AOSP+MPTCP with integrated Google Apps
Run:

```
$repo init -u https://github.com/multipath-tcp/android.git -b gapps
$repo sync -j4
```
After synchronising the repo you need to run from the root directory of the repository:
  
```
$./script/enhanceAOSP -gapps
```
##### Only the AOSP with MPTCP:

```
$repo init https://github.com/multipath-tcp/android.git
$repo sync -j4
```

### Update the bootloader (if Android 4.1 is not installed)
* Download and extract https://developers.google.com/android/nexus/images#sojujzo54k
* You will need ```fastboot``` installed ( as mentioned here https://developers.google.com/android/nexus/images#instructions - you can take the binaries from the SDK)
* You need to delete the last line beginning with 'fastboot' in ```flash-all.sh``` and then execute it.
Afterwards you need to do as mentioned in http://source.android.com/source/building-devices.html#obtaining-proprietary-binaries

## Building
Simply run:
```
$source build/envsetup.sh
$lunch full_crespo-userdebug
$make -j4
```

## Installation
Turn the Nexus S to fastboot mode (turn it of and then on again using Volume Up and Power), connect it and then run:
```
$fastboot -w flashall
```
### About the project
The main part is the kernel (prebuilt included, sources available at [Multipath TCP kernel](https://github.com/multipath-tcp/mptcp_3.0.x/tree/mptcp_samsung) ), which is a port from the linux kernel implementation for [MPTCP](https://github.com/multipath-tcp/mptcp).
To enable 3G and WIFI the Android Connection Manager had to be changed (in android_framework_base).
To setup routes automatically for both interfaces the Network Daemon had to be changed (in android_system_netd).
And to enable the [MPTCPControl app](https://github.com/mptcp-galaxys2) the iproute2 package hat to be enhanced in order to support MPTCP specific commands (in android_external_iproute2).

#### Acknowledgments:
This work was partially supported by the German BMBF within the project SKIMS.

Contact: Please, send any suggestions, bugs, and questions to [Raphael Wutzke](mailto:raphael.wutzke@googlemail.com)
