I did some black magic here to OSX libs to build. I used this to build them:

cd Soft/Build/; make RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=x86_64 USE_MACOSX=yes; cd -
cd Soft/Build/; make RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=i386 USE_MACOSX=yes; cd -

You can also clean them like this

cd Soft/Build/; make clean RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=x86_64 USE_MACOSX=yes; cd -;
cd Soft/Build/; make clean RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=i386 USE_MACOSX=yes; cd -;
rm -rf Soft/Build/targets_versions

I then lipo'd them LIKE A BOSS

lipo -arch i386 Soft/Build/targets_versions/vlib_DEBUG_MODE_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libvlib.a -arch x86_64 Soft/Build/targets_versions/vlib_DEBUG_MODE_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libvlib.a -create -output ./libvlib.a
lipo -arch i386 Soft/Build/targets_versions/sdk_DEBUG_MODE_vlib_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libsdk.a -arch x86_64 Soft/Build/targets_versions/sdk_DEBUG_MODE_vlib_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libsdk.a -create -output ./libsdk.a
lipo -arch i386 Soft/Build/targets_versions/ardrone_lib_DEBUG_MODE_vlib_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libpc_ardrone.a -arch x86_64 Soft/Build/targets_versions/ardrone_lib_DEBUG_MODE_vlib_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libpc_ardrone.a -create -output ./libpc_ardrone.a


All together now

cd Soft/Build/; make clean RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=x86_64 USE_MACOSX=yes; cd -;
cd Soft/Build/; make clean RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=i386 USE_MACOSX=yes; cd -;
rm -rf Soft/Build/targets_versions
cd Soft/Build/; make RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=x86_64 USE_MACOSX=yes; cd -
cd Soft/Build/; make RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=i386 USE_MACOSX=yes; cd -
lipo -arch i386 Soft/Build/targets_versions/vlib_DEBUG_MODE_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libvlib.a -arch x86_64 Soft/Build/targets_versions/vlib_DEBUG_MODE_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libvlib.a -create -output ./libvlib.a
lipo -arch i386 Soft/Build/targets_versions/sdk_DEBUG_MODE_vlib_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libsdk.a -arch x86_64 Soft/Build/targets_versions/sdk_DEBUG_MODE_vlib_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libsdk.a -create -output ./libsdk.a
lipo -arch i386 Soft/Build/targets_versions/ardrone_lib_DEBUG_MODE_vlib_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libpc_ardrone.a -arch x86_64 Soft/Build/targets_versions/ardrone_lib_DEBUG_MODE_vlib_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libpc_ardrone.a -create -output ./libpc_ardrone.a
mv *.a ../../../Kinect/KinectWings/Libraries/