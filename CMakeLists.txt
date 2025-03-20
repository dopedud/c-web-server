cmake_minimum_required(VERSION 3.10)

# set C standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED True)

# set directory path to C compiler
set(CMAKE_C_COMPILER "C:/msys64/mingw64/bin/gcc.exe")

project(C-WebServer VERSION 1.0 LANGUAGES C)

# set compiler flags
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall")

# main server executable
set(SERVER_SOURCES
    src/server.c
    src/net.c
    src/file.c
    src/mime.c
    src/cache.c
    src/hashtable.c
    src/llist.c
)

# add server source files to server executable
add_executable(server ${SERVER_SOURCES})

# Test executable
add_executable(cache_tests 
    src/cache_tests/cache_tests.c
    src/cache.c
    src/hashtable.c
    src/llist.c
)

# Custom target for running tests
add_custom_target(test
    COMMAND ${CMAKE_COMMAND} -E echo "Running cache tests..."
    COMMAND sh ${CMAKE_CURRENT_SOURCE_DIR}/src/cache_tests/runtests.sh
    DEPENDS cache_tests
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)