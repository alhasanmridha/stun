add_executable(client clientmain.cpp)
target_link_libraries(
  client ${CMAKE_PROJECT_NAME}_common ${CMAKE_PROJECT_NAME}_stuncore
  ${CMAKE_PROJECT_NAME}_networkutils)
