include_directories( . linux )
link_libraries(simdjson-windows-headers test-data)


if (TARGET benchmark::benchmark)
  add_executable(bench_sax bench_sax.cpp)
  target_link_libraries(bench_sax PRIVATE simdjson-internal-flags simdjson-include-source benchmark::benchmark)
endif (TARGET benchmark::benchmark)

link_libraries(simdjson simdjson-flags)
add_executable(benchfeatures benchfeatures.cpp)
add_executable(get_corpus_benchmark get_corpus_benchmark.cpp)
add_executable(perfdiff perfdiff.cpp)
add_executable(parse parse.cpp)
add_executable(parse_stream parse_stream.cpp)
add_executable(statisticalmodel statisticalmodel.cpp)

add_executable(parse_noutf8validation parse.cpp)
target_compile_definitions(parse_noutf8validation PRIVATE SIMDJSON_SKIPUTF8VALIDATION)
add_executable(parse_nonumberparsing parse.cpp)
target_compile_definitions(parse_nonumberparsing PRIVATE SIMDJSON_SKIPNUMBERPARSING)
add_executable(parse_nostringparsing parse.cpp)
target_compile_definitions(parse_nostringparsing PRIVATE SIMDJSON_SKIPSTRINGPARSING)

if (TARGET competition-all)
  add_executable(distinctuseridcompetition distinctuseridcompetition.cpp)
  target_link_libraries(distinctuseridcompetition PRIVATE competition-core)

  add_executable(minifiercompetition minifiercompetition.cpp)
  target_link_libraries(minifiercompetition PRIVATE competition-core)

  add_executable(parseandstatcompetition parseandstatcompetition.cpp)
  target_link_libraries(parseandstatcompetition PRIVATE competition-core)

  add_executable(parsingcompetition parsingcompetition.cpp)
  target_link_libraries(parsingcompetition PRIVATE competition-core)

  add_executable(allparsingcompetition parsingcompetition.cpp)
  target_link_libraries(allparsingcompetition PRIVATE competition-all)
  target_compile_definitions(allparsingcompetition PRIVATE ALLPARSER)
endif()

if (TARGET benchmark::benchmark)
  link_libraries(benchmark::benchmark)
  add_executable(bench_parse_call bench_parse_call.cpp)
  add_executable(bench_dom_api bench_dom_api.cpp)
  add_executable(bench_ondemand bench_ondemand.cpp)
endif()

include(checkperf.cmake)
