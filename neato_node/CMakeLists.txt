cmake_minimum_required(VERSION 2.8.3)
project(neato_node)

find_package(catkin REQUIRED)
catkin_package(DEPENDS)

install(FILES
  launch/bringup.launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

catkin_install_python(PROGRAMS
  nodes/neato.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
