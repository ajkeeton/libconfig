set(CMAKE_C_FLAGS "-Wall -Wshadow -Wextra -Wdeclaration-after-statement -Wno-unused-parameter")

include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}/../tinytest
  ${CMAKE_CURRENT_SOURCE_DIR}/../lib
)

link_directories(
  ${CMAKE_CURRENT_BINARY_DIR}/tinytest
  ${CMAKE_CURRENT_BINARY_DIR}/lib
)

add_executable(libconfig_tests
  tests.c
)

target_link_libraries(libconfig_tests
  tinytest
  config++
)
