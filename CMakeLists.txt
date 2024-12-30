cmake_minimum_required(VERSION 3.8)
project(realistic_error_generation_interfaces)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

set (ROS1_depends sensor_msgs)

find_package (catkin QUIET
  COMPONENTS message_generation ${ROS1_depends})

# ROS 1
if (catkin_FOUND)
	## Generate services in the 'srv' folder
	add_service_files (
	FILES
	ObtainError.srv
	)

	## Generate added messages and services with any dependencies listed here
	generate_messages (DEPENDENCIES ${ROS1_depends})

	catkin_package (
	CATKIN_DEPENDS message_runtime ${ROS1_depends}
	)

# ROS 2
else (catkin_FOUND)
	find_package(ament_cmake REQUIRED)
	find_package(sensor_msgs REQUIRED)
	find_package(rosidl_default_generators REQUIRED)

	rosidl_generate_interfaces(${PROJECT_NAME}
	  "srv/ObtainError.srv"
	  DEPENDENCIES sensor_msgs 
	)

	ament_package()

endif (catkin_FOUND)
