set(SOURCES 
testatomichelpers.cpp
testbuilder.cpp
testclientlogic.cpp
testcmdline.cpp
testcode.cpp
testdatastream.cpp
testfasthash.cpp
testintegrity.cpp
testmessagehandler.cpp
testpolling.cpp
testratelimiter.cpp
testreader.cpp
testrecvfromex.cpp)

add_executable(test ${SOURCES})
target_link_libraries(
  test ${CMAKE_PROJECT_NAME}_common ${CMAKE_PROJECT_NAME}_stuncore
  ${CMAKE_PROJECT_NAME}_networkutils)
