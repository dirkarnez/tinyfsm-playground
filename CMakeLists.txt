cmake_minimum_required(VERSION 3.14)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(tinyfsm-playground)

add_library(tinyfsm INTERFACE IMPORTED)

set_property(
  TARGET tinyfsm APPEND PROPERTY IMPORTED_CONFIGURATIONS DEBUG
)

set_property(
  TARGET tinyfsm APPEND PROPERTY IMPORTED_CONFIGURATIONS RELEASE
)

set_target_properties(tinyfsm PROPERTIES
  MAP_IMPORTED_CONFIG_MINSIZEREL Release
  MAP_IMPORTED_CONFIG_RELWITHDEBINFO Release
)

SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static")

target_include_directories(tinyfsm INTERFACE "${TINYFSM_ROOT}/include")

add_executable(${PROJECT_NAME} 
    "src/elevator.cpp"
    "src/elevator.hpp"
    "src/fsmlist.hpp"
    "src/main.cpp"
    "src/motor.cpp"
    "src/motor.hpp"
)

target_link_libraries(${PROJECT_NAME} tinyfsm)