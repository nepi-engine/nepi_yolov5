cmake_minimum_required(VERSION 3.5)
project(nepi_yolov5)

# Set c++11 cmake flags
set(CMAKE_CXX_FLAGS "-std=c++11 -Wall -Wno-unused-result -Wno-unknown-pragmas -Wno-unused-variable -fPIC -fpermissive ${CMAKE_CXX_FLAGS}")

# Define path of yolov5 folder here.
set(YOLOV5_PATH ${CMAKE_CURRENT_SOURCE_DIR}/yolov5)

# Data label images are installed below -- use that location for the compiled-in path to
# avoid being dependent on the source folder at build time
set( YOLOV5_FILE_INSTALL_FOLDER
  # Must hard-code it because CATKIN_GLOBAL_SHARE_DESTINATION is not yet defined at this point
  # ${CATKIN_GLOBAL_SHARE_DESTINATION}/yolov5
  /opt/nepi/nepi_engine/share/yolov5
)
message(WARNING "Installing yolov5 files to hard-coded ${YOLOV5_FILE_INSTALL_FOLDER}")
add_definitions(-D YOLOV5_FILE_PATH="${YOLOV5_FILE_INSTALL_FOLDER}")


# Find required packages
find_package(catkin REQUIRED COMPONENTS
std_msgs
)

catkin_package(
  CATKIN_DEPENDS
    rospy
    std_msgs
)


## Mark other files for installation (e.g. launch and bag files, etc.)
set( YOLOV5_INSTALL_FOLDER 
  # Must hard-coded 
  /opt/nepi/nepi_engine/share/yolov5
)
install(DIRECTORY   yolov5/
  DESTINATION ${YOLOV5_INSTALL_FOLDER}
  PATTERN "*git*" EXCLUDE
)



