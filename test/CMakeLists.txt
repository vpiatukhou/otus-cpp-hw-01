add_executable(libTests libTests.cpp)

if(WIN32)
    #used to find Boost
    set(CMAKE_FIND_LIBRARY_PREFIXES "lib")
endif()

find_package(Boost COMPONENTS REQUIRED unit_test_framework)

target_include_directories(libTests PRIVATE ${Boost_INCLUDE_DIRS} ${CMAKE_SOURCE_DIR}/src)

message("${Boost_LIBRARIES}")
target_link_libraries(libTests PRIVATE ${Boost_LIBRARIES} helloworld)

enable_testing()
add_test(NAME libTests COMMAND libTests)