project(OMP-Network LANGUAGES CXX DESCRIPTION "Non-stable network classes to use alongside the SDK" VERSION 2)

add_library(OMP-Network STATIC)

target_link_libraries(OMP-Network PUBLIC OMP-SDK)

target_include_directories(OMP-Network PUBLIC .)

file(GLOB_RECURSE network_source_list "*.cpp" "*.hpp")

set_property(TARGET OMP-Network PROPERTY SOURCES ${network_source_list})
set_property(TARGET OMP-Network PROPERTY POSITION_INDEPENDENT_CODE ON)

# Force /MD, as debug CRT for malloc/free are incompatible with open.mp
if (MSVC)
    set_property(TARGET OMP-Network PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreadedDLL")
endif()