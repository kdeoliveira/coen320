cmake_minimum_required(VERSION 3.0.0)
project(rtos_vehicule_monitoring VERSION 0.1.0)

add_executable(${PROJECT_NAME} main.cpp)

if(DEFINED QNX_PROCESSOR)
    add_definitions(-D_QNX_x86_64)
    add_definitions(-DDATASET_PATH="/opt/apps/dataset.csv")
else()


add_definitions(-DDATASET_PATH="${CMAKE_CURRENT_SOURCE_DIR}/data/dataset.csv")
endif()


if(CMAKE_BUILD_TYPE MATCHES Debug)
    message("Building in debug mode")
    add_definitions(-DDEBUG)
endif()



include(CTest)
enable_testing()

add_subdirectory(lib)
add_subdirectory(src)


set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

target_link_libraries(
    ${PROJECT_NAME} rtos_ipc
)