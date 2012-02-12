I did some black magic here to OSX libs to build. I used this to build them:

cd Soft/Build/; make RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=x86_64 USE_MACOSX=yes; cd -
cd Soft/Build/; make RELEASE_BUILD=no ARDRONE_TARGET_OS=macosx ARDRONE_TARGET_ARCH=i386 USE_MACOSX=yes; cd -

I then lipo'd them LIKE A BOSS

lipo -arch i386 Soft/Build/targets_versions/vlib_DEBUG_MODE_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libvlib.a -arch x86_64 Soft/Build/targets_versions/vlib_DEBUG_MODE_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libvlib.a -create -output ./libvlib.a
lipo -arch i386 Soft/Build/targets_versions/sdk_DEBUG_MODE_vlib_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libsdk.a -arch x86_64 Soft/Build/targets_versions/sdk_DEBUG_MODE_vlib_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libsdk.a -create -output ./libsdk.a
lipo -arch i386 Soft/Build/targets_versions/ardrone_lib_DEBUG_MODE_vlib_i386_Darwin_11.2.0_Developerusrbingcc_4.2.1/libpc_ardrone.a -arch x86_64 Soft/Build/targets_versions/ardrone_lib_DEBUG_MODE_vlib_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/libpc_ardrone.a -create -output ./libpc_ardrone.a

I have a hack in VLIB/video_config.h and VLIB/Platform/x86/video_config.h. For some reason TARGET_CPU_X86 isn't getting defined though it seems to be correctly passed into the compiler. Perhaps it's an LLVM-GCC bug? You can see that it's clearly getting defined in the compiler command:

/Developer/usr/bin/gcc -D_MOBILE -DRECORD_VIDEO -DGNU_LINUX  -DAT_MESSAGES_HEADER="\"../Common/at_msgs.h\"" -DUSE_NEW_ATCODEC -Wall -Wall  -g -O0 -DDEBUG_MODE -DDEBUG -D_DEBUG -D__linux__ -D__MACOSX__ -std=gnu99 -arch x86_64 -DTARGET_CPU_ARM=0 -DTARGET_CPU_X86=1 -DUSE_WIFI -DUSE_VLIB  -I../..//Soft/Common -I../..//Soft/Lib -I../../VLIB/.. -I../../VLIB/P263 -I../../VLIB/Platform/x86 -I../../Soft/Build/targets_versions/_Darwin_11.2.0_Developerusrbingcc_4.2.1/include -I../ -I..//VP_Com -I..//VP_Os/linux -I..//VP_Com/linux -I/specific -c -o ../../Soft/Build/targets_versions/vlib_DEBUG_MODE_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/video_codec.o ../../VLIB/video_codec.c 2>&1 >> ../../Soft/Build/targets_versions/vlib_DEBUG_MODE_x86_64_Darwin_11.2.0_Developerusrbingcc_4.2.1/build.log