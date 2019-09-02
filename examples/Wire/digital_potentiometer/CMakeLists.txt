# Note: in a totally seperate project, you will need something like this:

# include(FetchContent)
# set(FETCHCONTENT_QUIET 0)
# FetchContent_Declare(
#   RaspiArduino
#   GIT_REPOSITORY https://github.com/konsumer/RasPiArduino.git
#   GIT_TAG master
#   GIT_PROGRESS 1
#   GIT_SHALLOW 1
# )
# FetchContent_MakeAvailable(RaspiArduino)

add_executable(example_wire_digital_potentiometer digital_potentiometer.cpp)
target_link_libraries(example_wire_digital_potentiometer RaspiArduino)