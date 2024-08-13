cmake_minimum_required(VERSION 3.24...3.25)

add_library(mac-avcapture-legacy MODULE)
add_library(OBS::avcapture-legacy ALIAS mac-avcapture-legacy)

target_sources(mac-avcapture-legacy PRIVATE legacy/av-capture.mm legacy/left-right.hpp legacy/scope-guard.hpp)
target_include_directories(mac-avcapture-legacy PRIVATE legacy)

target_link_libraries(
  mac-avcapture-legacy
  PRIVATE OBS::libobs
          "$<LINK_LIBRARY:FRAMEWORK,AVFoundation.framework>"
          "$<LINK_LIBRARY:FRAMEWORK,Cocoa.framework>"
          "$<LINK_LIBRARY:FRAMEWORK,CoreFoundation.framework>"
          "$<LINK_LIBRARY:FRAMEWORK,CoreMedia.framework>"
          "$<LINK_LIBRARY:FRAMEWORK,CoreVideo.framework>"
          "$<LINK_LIBRARY:FRAMEWORK,CoreMediaIO.framework>")

set_target_properties_obs(
  mac-avcapture-legacy
  PROPERTIES FOLDER plugins
             PREFIX ""
             XCODE_ATTRIBUTE_CLANG_ENABLE_OBJC_ARC YES
             XCODE_ATTRIBUTE_CLANG_WARN_SUSPICIOUS_IMPLICIT_CONVERSION YES
             XCODE_ATTRIBUTE_GCC_WARN_SHADOW YES)
