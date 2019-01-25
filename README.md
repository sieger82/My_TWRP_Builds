## QUICK Guide ##
-----------------

### establish build environment

references:
https://developer.sony.com/develop/open-devices/guides/aosp-build-instructions/build-aosp-nougat-8-1-oreo-4-4 and https://source.android.com/setup/build/initializing

```bash
#remove old java
sudo apt-get purge openjdk-* icedtea-* icedtea6-*

#install correct java
sudo apt-get update
sudo apt-get install openjdk-8-jdk

#install tools
sudo apt-get install bison g++-multilib git gperf libxml2-utils make zlib1g-dev:i386 zip liblz4-tool libncurses5
sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc unzip
sudo apt-get install python-networkx libnss-sss:i386

#download repo tool
mkdir ~/bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo

#set path for repo tool (don't do multiple times!)
echo export PATH=~/bin:$PATH >> ~/.bashrc

#reload bash for current shell
source ~/.bashrc
```

### create folder for the tree and init repo

```bash
mkdir TWRP-build-env-8.1
repo init --depth=1 -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-8.1
repo sync

#link local manifests.
#in .repo dir do:
ln -s <path_to_dir_with_local_manifests> local_manifests

#then again
repo sync
```

### build
```bash
#!/bin/bash
cd ~/src/TWRP-build-env-8.1
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
. build/envsetup.sh
lunch omni_<device>-eng
make -j4 recoveryimage
```



