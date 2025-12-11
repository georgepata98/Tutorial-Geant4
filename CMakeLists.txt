cmake_minimum_required(VERSION 3.16...3.27)
project(Tutorial)

option(WITH_GEANT4_UIVIS "Build with Geant4 UI and Vis drivers" ON)
if(WITH_GEANT4_UIVIS)
    find_package(Geant4 REQUIRED ui_all vis_all)
else()
    find_package(Geant4 REQUIRED)
endif()

include(${Geant4_USE_FILE})
include_directories(${PROJECT_SOURCE_DIR}/include)

file(GLOB_RECURSE sources ${PROJECT_SOURCE_DIR}/*.cc)
file(GLOB_RECURSE headers ${PROJECT_SOURCE_DIR}/*.hh)

add_executable(sim main.cc ${sources} ${headers})
target_link_libraries(sim ${Geant4_LIBRARIES})

add_custom_target(Tutorial DEPENDS sim)
