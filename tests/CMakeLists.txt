# --- unit tests ---
function(add_bw64_test name)
  add_executable(${name} ${name}.cpp)
  target_link_libraries(${name}
    PRIVATE
    libbw64
    Boost::boost
  )
  add_test(
    NAME ${name}
    COMMAND $<TARGET_FILE:${name}>
    WORKING_DIRECTORY ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}
  )
endfunction()

# copy test files so unit test can find them relative to their running location
# when executed as "test" target
if(CMAKE_RUNTIME_OUTPUT_DIRECTORY)
  file(COPY ${PROJECT_SOURCE_DIR}/testfiles DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})
else()
  file(COPY ${PROJECT_SOURCE_DIR}/testfiles DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
endif()

add_bw64_test(utils_tests)
add_bw64_test(chunk_tests)
add_bw64_test(file_tests)
