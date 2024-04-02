> [!WARNING]  
> I am still working on this, and it doesn't work at all, yet

This is a fork of [RasPiArduino](https://github.com/konsumer/RasPiArduino). That project's purpose is to treat a pi exactly like an Arduino, using plain IDE, over the network. If you want to do that, use theirs.

The idea here is that you can use Arduino API, outside of the IDE, to make code very similar to Arduino (and share device-driver libs) with C++ or C.

## motivation

I needed to make some native Pi stuff in C (puredata extensions that can mess with hardware.) There is [pigpio](https://abyz.me.uk/rpi/pigpio/) and [wiringPi](https://github.com/WiringPi/WiringPi), which are both great, but I wanted to reuse existing Arduino device-libs for a few things, so I didn't have to write them from scratch in those libs.

## setup

Start with Raspberry Pi OS Lite. Here are some preperation-steps for your pi, that will increase overall performance:

```
# get root
sudo -s

# disable serial console
systemctl disable serial-getty@ttyAMA0
sed -i "s|console=/dev/ttyAMA0||" /boot/firmware/cmdline.txt

# disable obnboard audio
sed -i "s|dtparam=audio=on|#dtparam=audio=on|" /boot/firmware/config.txt  
```

On pizero & pi4, I also like to [enable gadget mode](https://www.hardill.me.uk/wordpress/2019/11/02/pi4-usb-c-gadget/), so I can SSH into it, without wifi.

## usage

If you are using cmake, you can include it in your project like this:

```cmake
include(FetchContent)
set(FETCHCONTENT_QUIET 0)

FetchContent_Declare(
  RaspiArduino
  GIT_REPOSITORY https://github.com/konsumer/RasPiArduino.git
  GIT_TAG master
  GIT_PROGRESS 1
  GIT_SHALLOW 1
)
FetchContent_MakeAvailable(RaspiArduino)
```

It static-compiles, so your program will have no dependencies.

Then use it with your targets, like this:

```cmake
add_executable(mycoolprogram src/main.c)
target_link_libraries(mycoolprogram RaspiArduino)
```

## dev

To test, do this:

```
cmake -B build
cmake --build build
```

## todo

- actually get it building
- add standalone examples (using cmake) for everyting. [Here](examples/Wire/digital_potentiometer) is my first example.
- add plain C wrapper to whole lib (for using in plain C)
- lots of testing
- hardware emulators that use SDL (for use on desktop)
