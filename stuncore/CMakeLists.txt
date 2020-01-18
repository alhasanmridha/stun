set(BINARY ${CMAKE_PROJECT_NAME}_stuncore)
set(SOURCES
    buffer.cpp
    datastream.cpp
    messagehandler.cpp
    socketaddress.cpp
    stunbuilder.cpp
    stunclientlogic.cpp
    stunclienttests.cpp
    stunreader.cpp
    stunutils.cpp)
include_directories(../common)
add_library(${BINARY} STATIC ${SOURCES})
target_link_libraries(${BINARY} PUBLIC ${CMAKE_PROJECT_NAME}_common)
