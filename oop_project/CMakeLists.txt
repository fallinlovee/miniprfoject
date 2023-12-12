# CMakeLists.txt : CMake project for oop_project, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("oop_project")

# Add source to this project's executable.
add_executable (oop_project "main.cpp" "oop_project.h" "date.h" "date.cpp" "human.h" "human.cpp" "student.h" "student.cpp" "publication.h" "publication.cpp" "research.h" "research.cpp")

# Include directories for the main project
target_include_directories(oop_project PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")

# Libraries

# Date library
add_library(Date
    "date.h"
    "date.cpp"
)

target_include_directories(Date PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(oop_project PRIVATE Date)

# Student library
add_library(Student
    "human.h"
    "human.cpp"
    "student.h"
    "student.cpp"
)

target_include_directories(Student PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(oop_project PRIVATE Student)

# Research library
add_library(Research
    "publication.h"
    "publication.cpp"
    "research.h"
    "research.cpp"
)

target_include_directories(Research PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(oop_project PRIVATE Research)

# Set C++ standard
if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET oop_project PROPERTY CXX_STANDARD 20)
endif()