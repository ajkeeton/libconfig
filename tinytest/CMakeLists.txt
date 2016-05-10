set(CMAKE_C_FLAGS "-Wall -Wshadow -Wextra -Wdeclaration-after-statement -Wno-unused-parameter")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
add_library(tinytest STATIC
  tinytest.c
)
