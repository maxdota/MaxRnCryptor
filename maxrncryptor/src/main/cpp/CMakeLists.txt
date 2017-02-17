cmake_minimum_required(VERSION 3.4.1)

add_library(rncryptor SHARED
            rncryptor-native.cpp rncryptor-native.h
            rncryptor.cpp rncryptor.h
            rndecryptor.cpp rndecryptor.h
            rnencryptor.cpp rnencryptor.h)

add_library(libcryptopp_shared SHARED IMPORTED)
set_target_properties(libcryptopp_shared PROPERTIES IMPORTED_LOCATION
    ${CMAKE_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}/libcryptopp_shared.so)


add_library(libgnustl_shared SHARED IMPORTED)
set_target_properties(libgnustl_shared PROPERTIES IMPORTED_LOCATION
    ${CMAKE_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}/libgnustl_shared.so)

# Include libraries needed for hello-jni lib
target_link_libraries(rncryptor
                      android
                      libcryptopp_shared
                      libgnustl_shared
                      log)

include_directories( imported-cryptopp/ )
include_directories( / )

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions -frtti" )
SET (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fexceptions -frtti")