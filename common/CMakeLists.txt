set(BINARY ${CMAKE_PROJECT_NAME}_common)
set(SOURCES 
atomichelpers.cpp 
cmdlineparser.cpp 
common.cpp fasthash.cpp 
getconsolewidth.cpp 
getmillisecondcounter.cpp 
logger.cpp prettyprint.cpp 
refcountobject.cpp 
stringhelper.cpp)

add_library(${BINARY} STATIC ${SOURCES})