cmake_minimum_required(VERSION 3.0.0)
project(test VERSION 0.1.0)

set(TARGET_NAME main)

set(Boost_USE_STATIC_LIBS OFF) 
set(Boost_USE_MULTITHREADED ON)  
set(Boost_USE_STATIC_RUNTIME OFF) 

cmake_policy(SET CMP0076 NEW)
set (CMAKE_CXX_STANDARD 17)

include_directories(${TRIPLET_INCLUDE_DIRS}) 

add_executable(${TARGET_NAME})

include_directories("./src/cpp")
add_subdirectory("./src/cpp")

# Adding Boost:
find_package(Boost 1.78.0)

# Adding SDL2:
find_package(SDL2 CONFIG REQUIRED)
target_link_libraries(main PRIVATE SDL2::SDL2 SDL2::SDL2main)

# Adding Imgui:
find_package(imgui CONFIG REQUIRED)
target_link_libraries(main PRIVATE imgui::imgui)

set_target_properties(${TARGET_NAME}
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "./arc/"
    LIBRARY_OUTPUT_DIRECTORY "./lib/"
    RUNTIME_OUTPUT_DIRECTORY "./bin/"
)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
