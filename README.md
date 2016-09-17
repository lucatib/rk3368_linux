# rk3368_linux
arm64 kernel rk3368

Build crossdev arm64:
crossdev --gcc =5.4.0 --genv 'USE="-fortran -mudflap -nls -openmp multilib -sanitize --with-float=hard"' -t aarch64-linux-gnu

cd kernel
CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm64 make geekbox_defconfig
CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm64 make Image modules

cd u-boot
make rk3368_box_defconfig
make -j16
cd ..

source ./build/envsetup.sh
lunch rk3368_64-userdebug
make -j16
