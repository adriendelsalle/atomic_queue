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

install(
    TARGETS atomic_queue
    EXPORT ${PROJECT_NAME}-targets
)

install(
    EXPORT ${PROJECT_NAME}-targets
    FILE ${PROJECT_NAME}Targets.cmake
    DESTINATION ${ATOMIC_QUEUE_CMAKECONFIG_INSTALL_DIR}
)

export(
    EXPORT ${PROJECT_NAME}-targets
    FILE ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Targets.cmake
)
