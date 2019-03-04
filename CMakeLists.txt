cmake_minimum_required(VERSION 3.11)
#set(CMAKE_CXX_STANDARD 11)

project(Gist)

file(GLOB FILES src/core/*.h src/core/*.cpp
					 src/mfcc/*.h src/mfcc/*.cpp
					 src/onset-detection-functions/*.h src/onset-detection-functions/*.cpp
					 src/pitch/*.h src/pitch/*.cpp
					 src/fft/WindowFunctions.h src/fft/WindowFunctions.cpp
					 src/*.h src/*.cpp)
					 
add_library(Gist STATIC ${FILES})

file(GLOB_RECURSE KFFT_FILES libs/kiss_fft130/*.h libs/kiss_fft130/*.c)
add_library(KFFT STATIC ${KFFT_FILES})
target_link_libraries(Gist PRIVATE KFFT)

target_compile_options(Gist PUBLIC -DUSE_KISS_FFT)