cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(TorchJack)

set(CMAKE_PREFIX_PATH /home/felix/Downloads/libtorch)


find_package(Torch REQUIRED COMPONETS
jack_msgs
)

INCLUDE(FindPkgConfig)
pkg_check_modules (JACK jack)
message( "Found jack: " ${JACK_FOUND} )

pkg_check_modules (SNDFILE sndfile)
message( "Found sndfile: " ${SNDFILE_FOUND} )
pkg_check_modules (SAMPLERATE samplerate)
message( "Found samplerate: " ${SAMPLERATE_FOUND} )

include_directories(
${JACK_INCLUDE_DIRS}
)



set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${TORCH_CXX_FLAGS}")

add_executable(${PROJECT_NAME} loadmodel.cpp)

target_link_libraries(${PROJECT_NAME} "${TORCH_LIBRARIES}" "${JACK_LIBRARIES}")

set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 14)
