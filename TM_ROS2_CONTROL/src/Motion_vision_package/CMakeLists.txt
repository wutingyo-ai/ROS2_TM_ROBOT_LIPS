cmake_minimum_required(VERSION 3.8)
project(Motion_vision_package)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

add_executable(TM_control_node src/TM_control_node.cpp)
target_include_directories(TM_control_node PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>)
target_compile_features(TM_control_node PUBLIC c_std_99 cxx_std_17)  # Require C99 and C++17

install(TARGETS TM_control_node
  DESTINATION lib/${PROJECT_NAME})

# ===== Python node =====
install(PROGRAMS
  scripts/robot_move.py
  DESTINATION lib/${PROJECT_NAME}
)


ament_package()
