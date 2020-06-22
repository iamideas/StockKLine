cmake_minimum_required(VERSION 3.5)

project(StockKLine LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# QtCreator supports the following variables for Android, which are identical to qmake Android variables.
# Check http://doc.qt.io/qt-5/deployment-android.html for more information.
# They need to be set before the find_package(Qt5 ...) call.

#if(ANDROID)
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#    if (ANDROID_ABI STREQUAL "armeabi-v7a")
#        set(ANDROID_EXTRA_LIBS
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libcrypto.so
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libssl.so)
#    endif()
#endif()

set(CMAKE_PREFIX_PATH ${QT_DIR})

find_package(Qt5 COMPONENTS Widgets LinguistTools REQUIRED)

set(TS_FILES myI18N_zh_CN.ts)


  add_executable(StockKLine
    main.cpp
    mainwindow.cpp
    mainwindow.h
    mainwindow.ui
    autogrid.cpp
    autogrid.h
    datafile.cpp
    datafile.h
    klinegrid.cpp
    klinegrid.h
    kvolumegrid.cpp
    kvolumegrid.h
    showdetail.cpp
    showdetail.h
    ${TS_FILES}
  )

target_link_libraries(StockKLine PRIVATE Qt5::Widgets)
set_target_properties(StockKLine PROPERTIES LINK_FLAGS "/SUBSYSTEM:WINDOWS /ENTRY:mainCRTStartup")
qt5_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})

add_custom_command(TARGET StockKLine POST_BUILD 
    COMMAND ${QT_DIR}/bin/windeployqt  --no-translations --no-system-d3d-compiler --no-opengl --no-svg ${CMAKE_CURRENT_BINARY_DIR}/Debug/StockKLine${CMAKE_EXECUTABLE_SUFFIX})