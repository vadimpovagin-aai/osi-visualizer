cmake_minimum_required(VERSION 3.1)
#add_subdirectory(open-simulation-interface)
project(osi-visualizer)

set(CMAKE_CXX_STANDARD 11)

set(CMAKE_PREFIX_PATH C:/Qt/5.11.1/msvc2015)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

#add_definitions(-DZMQ_STATIC)

find_package(Qt5 COMPONENTS Core Gui OpenGL Widgets Xml Network REQUIRED)

find_path(
  FMILIB_INCLUDE_DIRS
  fmilib.h
  HINTS ..\\3rdparty\\FMI\\include
)

find_library(
  FMILIB_LIBRARY
  fmilib_shared
  HINTS ..\\3rdparty\\FMI\\lib
)

set(SOURCES
    src/main.cpp
    src/mainwindow.cpp
    src/pythoncomparedialog.cpp
    src/displayobjectdialog.cpp
    src/glwidget.cpp
    src/globject.cpp
    src/camera.cpp
    src/tcpreceiver.cpp
    src/osireader.cpp
    src/glvehicle.cpp
    src/gllanemarking.cpp
    src/lane.cpp
    src/glgrid.cpp
    src/customtreewidgetitem.cpp
    src/gltriangle.cpp
    src/appconfig.cpp
    src/glpoint.cpp
    src/gltrafficsign.cpp
    src/qrc_resources.cpp
    src/osiparser.cpp
    src/glfieldofview.cpp
    src/fmureceiver.cpp
    src/utils.cpp

)

set(HEADERS
    include/mainwindow.h
    include/pythoncomparedialog.h
    include/displayobjectdialog.h
    include/glwidget.h
    include/globject.h
    include/camera.h
    include/imessagesource.h
    include/tcpreceiver.h
    include/osireader.h
    include/glvehicle.h
    include/gllanemarking.h
    include/lane.h
    include/glgrid.h
    include/types.h
    include/customtreewidgetitem.h
    include/gltriangle.h
    include/appconfig.h
    include/global.h
    include/glpoint.h
    include/gltrafficsign.h
    include/osiparser.h
    include/glfieldofview.h
    include/fmureceiver.h
    include/utils.h
)


include_directories(
    ${CMAKE_CURRENT_LIST_DIR}/include
    ${FMILIB_INCLUDE_DIRS}
    "..\\3rdparty\\osi\\include"
    "..\\3rdparty\\protobuf\\src"
    "..\\3rdparty\\cppzmq"
    "..\\3rdparty\\libzmq\\include"
)


add_executable(${PROJECT_NAME}
    ${HEADERS}
    ${SOURCES}
)

target_link_libraries(${PROJECT_NAME}
    Qt5::Core
    Qt5::Widgets
    Qt5::Xml
    Qt5::Gui
    Qt5::OpenGL
    Qt5::Network

    #open_simulation_interface
    "..\\..\\3rdparty\\osi\\lib\\open_simulation_interface_static.lib"
    ${FMILIB_LIBRARY}
    "..\\..\\3rdparty\\protobuf\\lib\\libprotobuf.lib"
    "..\\..\\3rdparty\\libzmq\\lib\\libzmq-v141-mt-4_3_1.lib"
       
    ws2_32.lib
    )

