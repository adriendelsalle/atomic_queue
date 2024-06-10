CMAKE_MINIMUM_REQUIRED( VERSION 3.25 )

PROJECT(atomic_queue VERSION 1.5.0)

OPTION( ATOMIC_QUEUE_BUILD_TESTS
    "If the tests should be built."
    OFF
)

OPTION( ATOMIC_QUEUE_BUILD_EXAMPLES
    "If examples should be built."
    OFF
)

include(GNUInstallDirs) 
include(CMakePackageConfigHelpers)

set(CMAKECONFIG_INSTALL_DIR "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}" CACHE
    STRING "install path for atomic_queueConfig.cmake")

configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/cmake/${PROJECT_NAME}Config.cmake.in
    "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
    INSTALL_DESTINATION ${CMAKECONFIG_INSTALL_DIR})

if ( PROJECT_IS_TOP_LEVEL )
    set(CMAKE_CXX_STANDARD 14)
    set(CMAKE_CXX_STANDARD_REQUIRED)
endif()

add_subdirectory( include )

if ( ATOMIC_QUEUE_BUILD_TESTS )
    enable_testing()
endif()

if ( ATOMIC_QUEUE_BUILD_TESTS OR ATOMIC_QUEUE_BUILD_EXAMPLES)
    add_subdirectory( src )
endif()

add_library(max0x7ba::atomic_queue ALIAS atomic_queue)