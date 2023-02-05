# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.8)

set(PROJECT_NAME "minesweeper")

project (${PROJECT_NAME})

add_subdirectory ("src")

file(GLOB_RECURSE RES_FILES CONFIGURE_DEPENDS "res/*")

add_executable (${PROJECT_NAME} WIN32 ${PROJECT_SOURCES} ${RES_FILES})
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 20)
set_source_files_properties(${RES_FILES} PROPERTIES HEADER_FILE_ONLY true)

get_filename_component(PROJECT_WORKING_DIR ${CMAKE_CURRENT_SOURCE_DIR} ABSOLUTE)
target_compile_definitions(${PROJECT_NAME} PRIVATE _AMD64_)

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME})

set(RISE_RESOURCE_DIRECTORY "${PROJECT_WORKING_DIR}/res/")

add_subdirectory ("dependencies")

target_link_libraries(${PROJECT_NAME} ${PROJECT_DEPENDENCIES})

target_include_directories(${PROJECT_NAME} PRIVATE "src")