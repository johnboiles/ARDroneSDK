ARDroneSDK
===========
http://github.com/johnboiles/ARDroneSDK

Fork of Parrot's official ARDrone SDK.

Additions / Changes Since Forking
---------------------------------
* Support for building ARDroneLib for OSX as a universal binary. However the 32 bit part is the only one that works. I've gotten the makefiles to the point where they will build 64 bit binaries for OSX, however they always seem to crash. I expect the code is doing something stupid that assumes a 32 bit system.

Building ARDroneLib for OSX
---------------------------
I used this to build them:

	cd ARDroneLib/Soft/Build/; make RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=x86_64 USE_MACOSX=yes; cd -
	cd ARDroneLib/Soft/Build/; make RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=i386 USE_MACOSX=yes; cd -

You can also clean them like this

	cd ARDroneLib/Soft/Build/; make clean RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=x86_64 USE_MACOSX=yes; cd -;
	cd ARDroneLib/Soft/Build/; make clean RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=i386 USE_MACOSX=yes; cd -;
	rm -rf ARDroneLib/Soft/Build/targets_versions

I then lipo them LIKE A BOSS

	lipo -arch i386 ARDroneLib/Soft/Build/targets_versions/vlib_DEBUG_MODE_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libvlib.a -arch x86_64 ARDroneLib/Soft/Build/targets_versions/vlib_DEBUG_MODE_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libvlib.a -create -output ./libvlib.a
	lipo -arch i386 ARDroneLib/Soft/Build/targets_versions/sdk_DEBUG_MODE_vlib_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libsdk.a -arch x86_64 ARDroneLib/Soft/Build/targets_versions/sdk_DEBUG_MODE_vlib_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libsdk.a -create -output ./libsdk.a
	lipo -arch i386 ARDroneLib/Soft/Build/targets_versions/ardrone_lib_DEBUG_MODE_vlib_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libpc_ardrone.a -arch x86_64 ARDroneLib/Soft/Build/targets_versions/ardrone_lib_DEBUG_MODE_vlib_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libpc_ardrone.a -create -output ./libpc_ardrone.a