find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)
bison_target(EcsParse ecsparse.y ${CMAKE_CURRENT_BINARY_DIR}/ecsparse.c)
flex_target(EcsScan ecsscan.l ${CMAKE_CURRENT_BINARY_DIR}/ecsscan.c)
include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})
add_executable(thecl
  ${BISON_EcsParse_OUTPUT_SOURCE} ${FLEX_EcsScan_OUTPUTS}
  expr.c thecl.c thecl06.c thecl10.c
  expr.h thecl.h)
target_link_libraries(thecl util)
install(TARGETS thecl DESTINATION bin)
install(FILES thecl.1 DESTINATION share/man/man1)
