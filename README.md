# MidiGurdy

The MidiGurdy is an electronic hurdy-gurdy. More information about the instrument can be found on
http://midigurdy.com and the support forum at https://forum.midigurdy.com

The repositories in this organization contain all the source code, configuration and sounds used
on the instrument. The code is split across multiple repositories:

* [midigurdy/mg-build](https://github.com/midigurdy/mg-build) - Configuration and scripts to build the MidiGurdy software stack
* [midigurdy/mg-core](https://github.com/midigurdy/mg-core) - The main program, sound generation, user-interface etc
* [midigurdy/mg-effects](https://github.com/midigurdy/mg-effects) - LADSPA effects used in the MidiGurdy sound output
* [midigurdy/mg-initialdata](https://github.com/midigurdy/mg-initialdata) - Default SoundFonts and configuration
* [midigurdy/mg-web](https://github.com/midigurdy/mg-web) - The web-interface of the MidiGurdy
* [midigurdy/linux](https://github.com/midigurdy/linux) - Linux kernel and special MidiGurdy drivers

This repository - midigurdy/midigurdy - does not contain any source code and is only used for documentation, wiki and issue tracker.

## Reporting Bugs or Feature Requests

If you notice a bug in any of the different components, please use the issue tracker in this repository.

If you have a new feature you would like to propose, please use the forum at
https://forum.midigurdy.com to discuss it with the other MidiGurdy users first.

## Building from source

The MidiGurdy build-process uses buildroot to cross-compile all code for the ARM architecture. The following
is a short introduction on how to compile it yourself or a recent Debian or Ubuntu system.

1. Make sure you have all required packages installed:
 ```
 sudo apt-get update
 sudo apt-get install --no-install-recommends -y git wget file python cpio unzip rsync bc build-essential \
           ca-certificates device-tree-compiler libncurses5-dev cmake npm libcap-dev imagemagick

 ```

2. Create a base-directory for all MidiGurdy related files:
 ```
 mkdir ~/mgurdy
 cd ~/mgurdy
 ```

3. Check out the midigurdy/mg-build repository:
 ```
 git clone https://github.com/midigurdy/mg-build.git
 ```

4. Create and configure the build environment:
 ```
 mg-build/scripts/create_build_environment.sh mg-build build
 ```

5. Switch to build environment and start the build
 ```
 cd build/output
 make
 ```
6. Sit back and wait for the build to finish... depending on your machine this will take between 30 minutes and a few hours.
 
7. Create the firmware update image
 ```
 ~/mgurdy/mg-build/scripts/build_system_image.sh ~/mgurdy/build/output/images
 ```
You will end up with a midigurdy-X.X.X.swu update file which you can store onto a USB stick and use to update the instrument.
