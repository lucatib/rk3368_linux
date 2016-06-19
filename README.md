# rk3368_linux
arm64 kernel rk3368

Build crossdev arm64:

crossdev --libc 2.21-r1 --binutils =9999 --gcc =4.9.3 --genv 'USE="-fortran -mudflap -nls -openmp multilib -sanitize"' -t aarch64-linux-gnu

export PATH=$PATH:/usr/x86_64-pc-linux-gnu/aarch64-linux-gnu/gcc-bin/4.9.3/
export CROSS_COMPILE=aarch64-linux-gnu-
export ARCH=arm64

make geekbox_defconfig
make -j16 Image modules
