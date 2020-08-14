cmake_minimum_required(VERSION 2.10)
project(CMake_Qt)
cmake_policy(VERSION 3.9)
FIND_PACKAGE(Qt5 COMPONENTS Core Gui Widgets Qml Quick REQUIRED)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -fPIC")

if(Qt5_FOUND)
	MESSAGE(STATUS "Qt5 Found.")
	SET(CMAKE_AUTOMOC ON) #autocompile QOBJECT  xx.cpp - > moc_xxx.cpp
	SET(CMAKE_AUTOUIC ON) #autocompile xx.ui -> ui_xx.h
	SET(CMAKE_AUTORCC ON) #autocompile qrc 
	SET(CMAKE_INCLUDE_CURRENT_DIR ON) # find moc_xxx ... files
#	INCLUDE_DIRECTORIES(${Qt5Core_INCLUDE_DIRS} 
#			    ${Qt5Xml_INCLUDE_DIRS}
#		            ${Qt5Gui_INCLUDE_DIRS} 
#			    ${Qt5Widgets_INCLUDE_DIRS}
#		            ${Qt5OpenGL_INCLUDE_DIRS})

        SET(QT_LIBRARIES ${Qt5Widgets_LIBRARIES} 
			 ${Qt5Core_LIBRARIES}
       			 ${Qt5Gui_LIBRARIES} 
			 ${Qt5Xml_LIBRARIES} )
	add_executable(${PROJECT_NAME} main.cpp mainwindow.cpp)
	TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${QT_LIBRARIES})
else()
	MESSAGE(ERROR "Qt5 Not Found.")
endif()

