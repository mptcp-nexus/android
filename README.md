Android 4.1.2 with MPTCP
========================

Currently only working with the Nexus S.

## Requirements
### Initialize build environment
See http://source.android.com/source/initializing.html

This may take a while. You can speed up the syncing and building using the -jn option, which will separate the task up into n threads.
* If the device shall have root access, run:

  ```
  $repo init -u https://github.com/multipath-tcp/android.git -b root
  $repo sync -j4
  ```
  * Google Apps will be installed automatically.
  * After synchronising the repo you need to run from the root directory of the repository:
  
  ```
  $./script -root
  ```
* If only the Google Apps shall be integrated you need to run:

  ```
  $repo init -u https://github.com/multipath-tcp/android.git -b gapps
  $repo sync -j4
  ```
  * After synchronising the repo you need to run from the root directory of the repository:
  
  ```
  $./script -gapps
  ```
* Otherwise you need to run:

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

### Installation
Turn the Nexus S to fastboot mode (turn it of and then on again using Volume Up and Power), connect it and then run:
```
$fastboot -w flashall
```

#### Acknowledgments:
This work was partially supported by the German BMBF within the project SKIMS.
Contact: Please, send any suggestions, bugs, and questions to [Raphael Wutzke](mailto:raphael.wutzke@googlemail.com)
