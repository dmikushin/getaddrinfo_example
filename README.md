# getaddrinfo() test for Android

Based on awesome gist by [Jiri Hnidek](https://gist.github.com/jirihnidek/bf7a2363e480491da72301b228b35d5d).

## Prerequsites

Create a standalone Android toolchain using the SDK script:

```
Android$ ./Sdk/ndk-bundle/build/tools/make_standalone_toolchain.py --arch arm --api 21 --install-dir ~/forge/android-toolchain
```

## Building

```
mkdir build
cd build
LDFLAGS=-static CFLAGS="-fPIC -O3 -fomit-frame-pointer -ffast-math -march=armv7-a" CC=$(pwd)/../../android-toolchain/bin/arm-linux-androideabi-gcc cmake ..
make
```

## Testing

```
adb push ./getaddrinfo_example /system/bin/
adb shell
/system/bin/getaddrinfo google.com
```

Output:

```
Host: google.com
IPv4 address: 172.217.168.78(google.com)
IPv6 address: 2a00:1450:400a:801::200e(google.com)
```
