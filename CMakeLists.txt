cmake_minimum_required(VERSION 2.8.3)
project(image_filtering_for_aruco)

find_package(catkin REQUIRED COMPONENTS 
	roscpp
    std_msgs 
	message_generation
	image_transport
	cv_bridge
)


find_package(OpenCV REQUIRED)

include_directories(${catkin_INCLUDE_DIRS})
include_directories(${PROJECT_SOURCE_DIR}/Sources/)
include_directories(${PROJECT_SOURCE_DIR}/Headers/)

SET(SOURCES ${PROJECT_SOURCE_DIR}/src/main.cpp
			${PROJECT_SOURCE_DIR}/Sources/filter.cpp
   )
SET(HEADERS ${PROJECT_SOURCE_DIR}/Headers/filter.h
   )

catkin_package(
  DEPENDS
  INCLUDE_DIRS
  CATKIN_DEPENDS roscpp message_runtime
  LIBRARIES
  roscpp
  image_transport
  cv_bridge
  cmake_modules
)

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})
add_dependencies(${PROJECT_NAME} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS} ${catkin_LIBRARIES})
