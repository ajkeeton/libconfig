add_definitions(
  -DPARSER_PREFIX=\"libconfig_yy\"
  -D_REENTRANT
  -DHAVE_NEWLOCALE
  -DHAVE_USELOCALE
  -DHAVE_FREELOCALE
)

set(CMAKE_C_FLAGS "-Wall -Wshadow -Wextra -Wdeclaration-after-statement -Wno-unused-parameter")

find_package(BISON)
find_package(FLEX)

BISON_TARGET(
  grammar
  grammar.y
  ${CMAKE_CURRENT_SOURCE_DIR}/y.tab.c
  COMPILE_FLAGS "-y -d -p libconfig_yy"
)

FLEX_TARGET(
  scanner 
  scanner.l
  ${CMAKE_CURRENT_SOURCE_DIR}/lex.yy.c
  COMPILE_FLAGS "--header-file=scanner.h --prefix=libconfig_yy"
)

ADD_FLEX_BISON_DEPENDENCY(scanner grammar)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
add_library(config++ SHARED
  libconfig.c
  ${BISON_grammar_OUTPUTS}
  ${FLEX_scanner_OUTPUTS}
  scanctx.c
  strbuf.c
  libconfigcpp.c++
)
