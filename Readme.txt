rkdeveloptool gives you a simple way to read/write rockusb device.let's start.

For Linux
compile and install
1 install libusb and libudev
	sudo apt-get install libudev-dev libusb-1.0-0-dev dh-autoreconf
2 go into root of rkdeveloptool
3.aclocal
4.autoreconf -i
5.autoheader
5.automake --add-missing
4 ./configure
5 make

For Mac
brew install automake autoconf libusb pkg-config git wget
git clone https://github.com/rockchip-linux/rkdeveloptool
cd rkdeveloptool
wget https://patch-diff.githubusercontent.com/raw/rockchip-linux/rkdeveloptool/pull/73.patch
wget https://patch-diff.githubusercontent.com/raw/rockchip-linux/rkdeveloptool/pull/85.patch
git am *.patch
autoreconf -i
./configure
make -j $(nproc)
cp rkdeveloptool /opt/homebrew/bin/

rkdeveloptool usage,input "rkdeveloptool -h" to see

example:
1.download kernel.img
sudo ./rkdeveloptool db RKXXLoader.bin    //download usbplug to device
sudo ./rkdeveloptool wl 0x8000 kernel.img //0x8000 is base of kernel partition,unit is sector.
sudo ./rkdeveloptool rd                   //reset device

compile error help
if you encounter the error like below:
./configure: line 4269: syntax error near unexpected token `LIBUSB1,libusb-1.0'
./configure: line 4269: `PKG_CHECK_MODULES(LIBUSB1,libusb-1.0)'

You should install pkg-config libusb-1.0:
	sudo apt-get install pkg-config libusb-1.0 
