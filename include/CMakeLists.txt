CMAKE_MINIMUM_REQUIRED( VERSION 3.25 )

add_library(
    atomic_queue
    INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}/atomic_queue/atomic_queue.h
    ${CMAKE_CURRENT_SOURCE_DIR}/atomic_queue/atomic_queue_mutex.h
    ${CMAKE_CURRENT_SOURCE_DIR}/atomic_queue/barrier.h
    ${CMAKE_CURRENT_SOURCE_DIR}/atomic_queue/defs.h
    ${CMAKE_CURRENT_SOURCE_DIR}/atomic_queue/spinlock.h
)

target_include_directories(
    atomic_queue
    INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include>
)


include(GNUInstallDirs) 
include(CMakePackageConfigHelpers)

set(CMAKECONFIG_INSTALL_DIR "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}" CACHE
    STRING "install path for atomic_queueConfig.cmake")

configure_package_config_file(${CMAKE_SOURCE_DIR}/cmake/${PROJECT_NAME}Config.cmake.in
    "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
    INSTALL_DESTINATION ${CMAKECONFIG_INSTALL_DIR})

install(
    TARGETS atomic_queue
    EXPORT ${PROJECT_NAME}-targets
)

install(
    EXPORT ${PROJECT_NAME}-targets
    FILE ${PROJECT_NAME}Targets.cmake
    DESTINATION ${CMAKECONFIG_INSTALL_DIR}
)

export(
    EXPORT ${PROJECT_NAME}-targets
    FILE ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Targets.cmake
)
