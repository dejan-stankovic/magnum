#
#   This file is part of Magnum.
#
#   Copyright © 2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018
#             Vladimír Vondruš <mosra@centrum.cz>
#
#   Permission is hereby granted, free of charge, to any person obtaining a
#   copy of this software and associated documentation files (the "Software"),
#   to deal in the Software without restriction, including without limitation
#   the rights to use, copy, modify, merge, publish, distribute, sublicense,
#   and/or sell copies of the Software, and to permit persons to whom the
#   Software is furnished to do so, subject to the following conditions:
#
#   The above copyright notice and this permission notice shall be included
#   in all copies or substantial portions of the Software.
#
#   THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#   IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#   FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL
#   THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#   LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
#   FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
#   DEALINGS IN THE SOFTWARE.
#

if(WITH_ANDROIDAPPLICATION)
    add_library(PlatformAndroidApplicationTest SHARED AndroidApplicationTest.cpp)
    target_link_libraries(PlatformAndroidApplicationTest PRIVATE MagnumAndroidApplication)
    set_target_properties(PlatformAndroidApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
    if(CMAKE_ANDROID_NDK)
        android_create_apk(PlatformAndroidApplicationTest AndroidManifest.xml)
    endif()
endif()

if(WITH_GLFWAPPLICATION)
    add_executable(PlatformGlfwApplicationTest GlfwApplicationTest.cpp)
    target_link_libraries(PlatformGlfwApplicationTest PRIVATE MagnumGlfwApplication)
    set_target_properties(PlatformGlfwApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
endif()

if(WITH_GLUTAPPLICATION)
    add_executable(PlatformGlutApplicationTest GlutApplicationTest.cpp)
    target_link_libraries(PlatformGlutApplicationTest PRIVATE MagnumGlutApplication)
    set_target_properties(PlatformGlutApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
endif()

if(WITH_GLXAPPLICATION)
    add_executable(PlatformGlxApplicationTest GlxApplicationTest.cpp)
    target_link_libraries(PlatformGlxApplicationTest PRIVATE MagnumGlxApplication)
    set_target_properties(PlatformGlxApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
endif()

if(WITH_SDL2APPLICATION)
    add_executable(PlatformSdl2ApplicationTest Sdl2ApplicationTest.cpp)
    target_link_libraries(PlatformSdl2ApplicationTest PRIVATE MagnumSdl2Application)
    set_target_properties(PlatformSdl2ApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
    if(CORRADE_TARGET_EMSCRIPTEN)
        # So we can spin up a webserver in the build dir for easy testing
        file(COPY
            ../EmscriptenApplication.js
            ../WebApplication.css
            Sdl2ApplicationTest.html
            DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
    elseif(CORRADE_TARGET_IOS OR CORRADE_TARGET_APPLE)
        # The plist is needed in order to mark the app as DPI-aware
        set_target_properties(PlatformSdl2ApplicationTest PROPERTIES
            MACOSX_BUNDLE_INFO_PLIST ${CMAKE_CURRENT_SOURCE_DIR}/Sdl2ApplicationTest.plist
            MACOSX_BUNDLE ON
            XCODE_ATTRIBUTE_CODE_SIGNING_REQUIRED "YES")
    endif()
endif()

if(WITH_XEGLAPPLICATION)
    add_executable(PlatformXEglApplicationTest XEglApplicationTest.cpp)
    target_link_libraries(PlatformXEglApplicationTest PRIVATE MagnumXEglApplication)
    set_target_properties(PlatformXEglApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
endif()

if(WITH_WINDOWLESSCGLAPPLICATION)
    add_executable(PlatformWindowlessCglApplicationTest WindowlessCglApplicationTest.cpp)
    target_link_libraries(PlatformWindowlessCglApplicationTest PRIVATE MagnumWindowlessCglApplication)
    set_target_properties(PlatformWindowlessCglApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
endif()

if(WITH_WINDOWLESSEGLAPPLICATION)
    add_executable(PlatformWindowlessEglApplicationTest WindowlessEglApplicationTest.cpp)
    target_link_libraries(PlatformWindowlessEglApplicationTest PRIVATE MagnumWindowlessEglApplication)
    set_target_properties(PlatformWindowlessEglApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
    if(CORRADE_TARGET_EMSCRIPTEN)
        # So we can spin up a webserver in the build dir for easy testing
        file(COPY
            ../WindowlessEmscriptenApplication.js
            ../WebApplication.css
            WindowlessEglApplicationTest.html
            DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
    endif()
endif()

if(WITH_WINDOWLESSGLXAPPLICATION)
    add_executable(PlatformWindowlessGlxApplicationTest WindowlessGlxApplicationTest.cpp)
    target_link_libraries(PlatformWindowlessGlxApplicationTest PRIVATE MagnumWindowlessGlxApplication)
    set_target_properties(PlatformWindowlessGlxApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
endif()

if(WITH_WINDOWLESSIOSAPPLICATION)
    add_executable(PlatformWindowlessIosApplicationTest WindowlessIosApplicationTest.cpp)
    target_link_libraries(PlatformWindowlessIosApplicationTest PRIVATE MagnumWindowlessIosApplication)
    set_target_properties(PlatformWindowlessIosApplicationTest PROPERTIES
        MACOSX_BUNDLE ON
        XCODE_ATTRIBUTE_CODE_SIGNING_REQUIRED "YES"
        FOLDER "Magnum/Platform/Test")
endif()

if(WITH_WINDOWLESSWGLAPPLICATION)
    add_executable(PlatformWindowlessWglApplicationTest WindowlessWglApplicationTest.cpp)
    target_link_libraries(PlatformWindowlessWglApplicationTest PRIVATE MagnumWindowlessWglApplication)
    set_target_properties(PlatformWindowlessWglApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
endif()

if(WITH_WINDOWLESSWINDOWSEGLAPPLICATION)
    add_executable(PlatformWindowlessWindowsEglApplicationTest WindowlessWindowsEglApplicationTest.cpp)
    target_link_libraries(PlatformWindowlessWindowsEglApplicationTest PRIVATE MagnumWindowlessWindowsEglApplication)
    set_target_properties(PlatformWindowlessWindowsEglApplicationTest PROPERTIES FOLDER "Magnum/Platform/Test")
endif()
