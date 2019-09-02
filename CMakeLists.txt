cmake_minimum_required(VERSION 3.18)

project(RaspiArduino
  DESCRIPTION "Arduino API on Raspi"
  HOMEPAGE_URL "https://github.com/konsumer/RasPiArduino"
  VERSION 0.0.1
)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# set this to FALSE to only build the library
option(BUILD_RASPIARDUINO_EXAMPLES "Build RaspiArduino examples" TRUE)

include_directories(
  "${CMAKE_CURRENT_LIST_DIR}/cores/piduino"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/Bridge/src"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/DHT22"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/DS3231"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/EEPROM"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/Ethernet/src"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/Ethernet/src/utility"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/NOKIA_LCD"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/SD/src"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/SD/src/utility"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/SPI"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/TTY"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/Wire"
  "${CMAKE_CURRENT_LIST_DIR}/libraries/Wire/utility"
  "${CMAKE_CURRENT_LIST_DIR}/variants/bplus"
)

add_library(RaspiArduino STATIC
  cores/piduino/Console.cpp
  cores/piduino/HardwareSerial.cpp
  cores/piduino/IPAddress.cpp
  cores/piduino/Print.cpp
  cores/piduino/Stream.cpp
  cores/piduino/WMath.cpp
  cores/piduino/WString.cpp
  cores/piduino/cbuf.cpp
  cores/piduino/idemonitor.c
  cores/piduino/piconsole.c
  cores/piduino/raspberry_pi_revision.c
  cores/piduino/stdlib_noniso.cpp
  cores/piduino/wiring.c
  cores/piduino/wiring_digital.c
  cores/piduino/wiring_ids.c
  cores/piduino/wiring_int.c
  cores/piduino/wiring_main.cpp
  cores/piduino/wiring_pulse.c
  cores/piduino/wiring_pwm.c
  cores/piduino/wiring_shift.c
  cores/piduino/wiring_thread.c
  libraries/Bridge/src/Bridge.cpp
  libraries/Bridge/src/BridgeClient.cpp
  libraries/Bridge/src/BridgeServer.cpp
  libraries/Bridge/src/BridgeUdp.cpp
  libraries/Bridge/src/FileIO.cpp
  libraries/Bridge/src/HttpClient.cpp
  libraries/Bridge/src/Mailbox.cpp
  libraries/Bridge/src/Process.cpp
  libraries/DHT22/DHT22.cpp
  libraries/DS3231/DS3231.cpp
  libraries/Ethernet/src/Dhcp.cpp
  libraries/Ethernet/src/Dns.cpp
  libraries/Ethernet/src/Ethernet.cpp
  libraries/Ethernet/src/EthernetClient.cpp
  libraries/Ethernet/src/EthernetServer.cpp
  libraries/Ethernet/src/EthernetUdp.cpp
  libraries/Ethernet/src/utility/socket.cpp
  libraries/Ethernet/src/utility/w5100.cpp
  libraries/NOKIA_LCD/NOKIA_LCD.cpp
  libraries/SD/src/File.cpp
  libraries/SD/src/SD.cpp
  libraries/SD/src/utility/Sd2Card.cpp
  libraries/SD/src/utility/SdFile.cpp
  libraries/SD/src/utility/SdVolume.cpp
  libraries/SPI/SPI.cpp
  libraries/TTY/TTY.cpp
  libraries/Wire/Wire.cpp
  libraries/Wire/utility/twi.c
)

# all examples are built here
if (BUILD_RASPIARDUINO_EXAMPLES)
  add_subdirectory(examples/Wire/digital_potentiometer)
endif()