cmake_minimum_required(VERSION 2.7)
####Подключаем Boost
find_package(Boost 1.58.0 COMPONENTS system date_time filesystem thread regex serialization)
if(NOT Boost_FOUND)
    message(FATAL_ERROR "Could not find boost!")
endif()
include_directories(${BOOST_INCLUDE_DIRS})
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(CMAKE_PREFIX_PATH "/opt/soft/qt/5.8/gcc_64/")#указать путь к  Qt
set(CMAKE_AUTOMOC ON)#Q_OBJECT - For use in the design of the mechanism of signals and slots.
set(CMAKE_AUTOUIC ON)#To support forms created with QtDesigner
find_package( Qt5Core REQUIRED )# equals *.pro QT += gui core
find_package( Qt5Widgets REQUIRED )#widgets
find_package( Qt5Network REQUIRED )#Network
find_package( Qt5Sql REQUIRED )#DBMS support
find_package( Qt5Xml REQUIRED )# Xml support
find_package( Qt5PrintSupport REQUIRED )# printer
find_package( Qt5OpenGL REQUIRED)# OpenGL
add_subdirectory(${PROJECT_SOURCE_DIR}/3rd-party/googletest/)#add google test directory
include_directories(${PROJECT_SOURCE_DIR}/3rd_party/googletest/googletest/include)
set(SOURCE_FILES main.cpp)
add_executable(YourApp ${SOURCE_FILES})
target_link_libraries(YourApp Qt5::Widgets Qt5::Core Qt5::Network
        Qt5::Sql Qt5::OpenGL  #Specify the libraries with which we will link the binary
        ${Boost_LIBRARIES}
        gtest)

