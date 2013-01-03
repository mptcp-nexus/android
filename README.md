Android 4.1.2 with MPTCP
========================

This is a Multipath TCP port for Android 4.1.2. Currently, it runs only on Nexus S.

## Requirements
### Initialize build environment
See http://source.android.com/source/initializing.html

The following may take a while. You can speed up the syncing and building using the -jn option, which will separate the task up into n threads.
For building there are three different options:
##### 1. The AOSP+MPTCP with Root Access (Google Apps are integrated automatically)
Run:

    $ repo init -u https://github.com/multipath-tcp/android.git -b root
    $ repo sync -j4

After synchronising the repo you need to run from the root directory of the repository:
  
    $ ./script/enhanceAOSP.sh -root

##### 2. The AOSP+MPTCP with integrated Google Apps
Run:

    $ repo init -u https://github.com/multipath-tcp/android.git -b gapps
    $ repo sync -j4

After synchronising the repo you need to run from the root directory of the repository:
  

    $ ./script/enhanceAOSP.sh -gapps

##### 3. Only the AOSP with MPTCP:

    $ repo init https://github.com/multipath-tcp/android.git
    $ repo sync -j4

### Update the bootloader (if Android 4.1 is not installed)
- Download and extract https://developers.google.com/android/nexus/images#sojujzo54k
- Install ```fastboot```  (cf., https://developers.google.com/android/nexus/images#instructions - you can use the binaries from the SDK)
- Delete the last line beginning with 'fastboot' in ```flash-all.sh```
- Execute ```flash-all.sh```
- Follow the instructions at http://source.android.com/source/building-devices.html#obtaining-proprietary-binaries

## Building
Simply run:

    $ source build/envsetup.sh
    $ lunch full_crespo-userdebug
    $ make -j4

## Installation
Turn the Nexus S to fastboot mode (turn it of and then on again using Volume Up and Power), connect it and then run:

    $ fastboot -w flashall

## About the project
The main part of the MPTCP for Android is the kernel (prebuilt included, sources available at [Multipath TCP kernel](https://github.com/multipath-tcp/mptcp_3.0.x/tree/mptcp_samsung)), which is a port from the Linux kernel implementation of [MPTCP] (https://github.com/multipath-tcp/mptcp).

To allow for full MPTCP expierence, the following extensions are included:
- A modified Android Connection Manager, which enables 3G and WiFi in parallel (in android_framework_base).
- A modified Network Daemon, which automatically configures routes for both interfaces (in android_system_netd).
- A modified iproute2 package to enable the [MPTCPControl app](https://github.com/mptcp-galaxys2) to support MPTCP specific commands (in android_external_iproute2).

#### Acknowledgments:
This work was partially supported by the German BMBF within the project [SKIMS] (http://skims.realmv6.org).

#### Contact: 
Please, send any suggestions, bugs, or questions to [Raphael Wutzke](mailto:raphael.wutzke@googlemail.com)
