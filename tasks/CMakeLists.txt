include(loggerTaskLib)

pkg_check_modules(RTT_Typelib REQUIRED rtt_typelib-${OROCOS_TARGET})
include_directories(${RTT_Typelib_INCLUDE_DIRS})
link_directories(${RTT_Typelib_LIBRARY_DIRS})

ADD_LIBRARY(${LOGGER_TASKLIB_NAME} SHARED 
    ${LOGGER_TASKLIB_SOURCES}
    Logfile.cpp)

TARGET_LINK_LIBRARIES(${LOGGER_TASKLIB_NAME}
    ${OrocosRTT_LIBRARIES}
    ${LOGGER_TASKLIB_DEPENDENT_LIBRARIES}
    ${RTT_Typelib_LIBRARIES})
SET_TARGET_PROPERTIES(${LOGGER_TASKLIB_NAME}
    PROPERTIES LINK_INTERFACE_LIBRARIES "${LOGGER_TASKLIB_INTERFACE_LIBRARIES}")

INSTALL(TARGETS ${LOGGER_TASKLIB_NAME}
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib/orocos)

INSTALL(FILES ${LOGGER_TASKLIB_HEADERS}
    DESTINATION include/orocos/logger)

