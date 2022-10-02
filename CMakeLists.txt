cmake_minimum_required(VERSION 3.2)

set(CMAKE_CXX_STANDARD 14)
set(PATCH_VERSION 1)
set(PROJECT_VERSION 0.0.${PATCH_VERSION})

project(helloworld VERSION ${PROJECT_VERSION})
enable_testing()

configure_file(version.h.in ${CMAKE_CURRENT_BINARY_DIR}/generated_sources/version.h @ONLY)

add_executable(helloworld_cli main.cpp lib.cpp)
add_executable(libTests libTests.cpp lib.cpp)

find_package(Boost)

target_include_directories(helloworld_cli PRIVATE ${Boost_INCLUDE_DIRS} ${CMAKE_CURRENT_BINARY_DIR}/generated_sources)
target_include_directories(libTests PRIVATE ${Boost_INCLUDE_DIRS} ${CMAKE_CURRENT_BINARY_DIR}/generated_sources)

add_test(NAME libTests COMMAND libTests)

install(TARGETS helloworld_cli RUNTIME DESTINATION bin)

set(CPACK_GENERATOR DEB)

set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT example@example.com)

include(CPack)