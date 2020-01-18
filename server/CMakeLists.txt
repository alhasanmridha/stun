set(SOURCES main.cpp sampleauthprovider.cpp server.cpp stunconnection.cpp
            stunsocketthread.cpp tcpserver.cpp)

add_executable(server ${SOURCES})
target_link_libraries(
  server ${CMAKE_PROJECT_NAME}_common ${CMAKE_PROJECT_NAME}_stuncore
  ${CMAKE_PROJECT_NAME}_networkutils)
