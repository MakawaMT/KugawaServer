cmake_minimum_required(VERSION 3.4.1)

include_directories(libnode/include/node/)
#Sets the minimum version of CMake required to build the native library.

add_library( libnode
             SHARED
             IMPORTED )

set_target_properties( # Specifies the target library.
                       libnode
                       # Specifies the parameter you want to define.
                       PROPERTIES IMPORTED_LOCATION
                       # Provides the path to the library you want to import.
                       ${CMAKE_SOURCE_DIR}/libnode/bin/${ANDROID_ABI}/libnode.so )

add_library( # Sets the name of the library.
             native-lib

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
src/main/cpp/native-lib.cpp )

target_link_libraries( # Specifies the target library.
                       native-lib
                       # Links imported library.
                       libnode
                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )
