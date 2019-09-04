
project(XJGARSDKDemoApp-Mac)

cmake_minimum_required(VERSION 2.8)


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11  -stdlib=libc++")
find_package(OpenCV REQUIRED)
include_directories(${OPENCV_INCLUDE_DIRS} ${CMAKE_CURRENT_LIST_DIR}  )
LINK_DIRECTORIES(${PROJECT_SOURCE_DIR})



################################# MACOS setting#################
set(CMAKE_OSX_DEPLOYMENT_TARGET "10.8")
IF(APPLE)

#find_package(GLEW REQUIRED)
#if (GLEW_FOUND)
#include_directories(${GLEW_INCLUDE_DIRS})
#link_libraries(${GLEW_LIBRARIES})
#endif()

#find_path(GLEW_INCLUDE_DIR GL/glew.h)
#include_directories($(GLEW_INCLUDE_DIR))
#include_directories(/usr/local/include)
#link_libraries( /usr/local/lib )

INCLUDE_DIRECTORIES(/usr/local/include)
INCLUDE_DIRECTORIES ( /System/Library/Frameworks )
FIND_LIBRARY(GLUT_LIBRARY GLUT )
FIND_LIBRARY(OpenGL_LIBRARY OpenGL )
FIND_LIBRARY(GLEW_LIBRARY GLEW )
MARK_AS_ADVANCED (
GLUT_LIBRARY
OpenGL_LIBRARY)
SET(EXTRA_LIBS ${GLUT_LIBRARY} ${OpenGL_LIBRARY})
ENDIF (APPLE)


ADD_EXECUTABLE(libXJGARSDKTest  
				test_XJGARSDK_freeglut.cpp
)
TARGET_LINK_LIBRARIES(libXJGARSDKTest
                ${OpenCV_LIBS}
liblibXJGARSDK.dylib
                ${GLUT_LIBRARY} ${OpenGL_LIBRARY}
${GLEW_LIBRARY}
				#glew32.lib

				)

# Create the app target
set_target_properties(libXJGARSDKTest PROPERTIES
MACOSX_BUNDLE_INFO_PLIST ${CMAKE_CURRENT_LIST_DIR}/Info.plist
)

