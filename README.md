# rk3368_linux
arm64 kernel rk3368

Build crossdev arm64:

crossdev --libc 2.21-r1 --binutils =9999 --gcc =4.9.3 --genv 'USE="-fortran -mudflap -nls -openmp multilib -sanitize"' -t aarch64-linux-gnu

#!/bin/bash
export PATH=$PATH:/usr/x86_64-pc-linux-gnu/aarch64-linux-gnu/gcc-bin/4.9.3/
export CROSS_COMPILE=aarch64-linux-gnu-
export ARCHV=aarch64
export ARCH=arm64
#export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
#export PATH=$JAVA_HOME/bin:$PATH
#export CLASSPATH=.:$JAVA_HOME/lib:$JAVA_HOME/lib/tools.jar

cd u-boot
make rk3368_box_defconfig
make -j16
cd ..

cd kernel
make geekbox_defconfig
make Image modules
cd ..

. build/envsetup.sh
lunch rk3368_64-userdebug
make -j16
