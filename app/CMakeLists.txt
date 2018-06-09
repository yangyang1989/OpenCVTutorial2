# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)
# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Werror")

# configure import libs
set(distribution_DIR ${CMAKE_SOURCE_DIR}/../sdk/native/)
add_library(libopencv_core STATIC IMPORTED)
set_target_properties(libopencv_core PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/staticlibs/${ANDROID_ABI}/libopencv_core.a)

add_library(libopencv_imgproc STATIC IMPORTED)
set_target_properties(libopencv_imgproc PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/staticlibs/${ANDROID_ABI}/libopencv_imgproc.a)

add_library(libopencv_features2d STATIC IMPORTED)
set_target_properties(libopencv_features2d PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/staticlibs/${ANDROID_ABI}/libopencv_features2d.a)

add_library(libtbb STATIC IMPORTED)
set_target_properties(libtbb PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/3rdparty/libs/${ANDROID_ABI}/libtbb.a)

add_library(libtegra_hal STATIC IMPORTED)
set_target_properties(libtegra_hal PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/3rdparty/libs/${ANDROID_ABI}/libtegra_hal.a)

add_library(libopencv_java3 SHARED IMPORTED)
set_target_properties(libopencv_java3 PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/libs/${ANDROID_ABI}/libopencv_java3.so)

add_library(libcpufeatures STATIC IMPORTED)
set_target_properties(libcpufeatures PROPERTIES IMPORTED_LOCATION
    ${distribution_DIR}/3rdparty/libs/${ANDROID_ABI}/libcpufeatures.a)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
             mixed_sample

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             src/main/cpp/mixed_sample.cpp )

# Searches for a specified prebuilt library and stores the path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

#find_library( # Sets the name of the path variable.
#              log-lib
#
#              # Specifies the name of the NDK library that
#              # you want CMake to locate.
#              log )


target_include_directories(mixed_sample PRIVATE
                           ${distribution_DIR}/jni/include)


# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( mixed_sample
                       log
                       android
                       libopencv_core
                       libopencv_imgproc
                       libopencv_features2d
                       libtbb
                       libtegra_hal
                       libopencv_java3
                       z
                       libcpufeatures
                       )