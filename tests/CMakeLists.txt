include(FetchContent)
#for test
FetchContent_Declare(
        doctest
        GIT_REPOSITORY https://gitee.com/acking-you/doctest.git
        GIT_TAG v2.4.9
        GIT_SHALLOW TRUE
)
FetchContent_MakeAvailable(doctest)

#for benchmark
FetchContent_Declare(
        nanobench
        GIT_REPOSITORY https://gitee.com/acking-you/nanobench.git
        GIT_TAG v4.1.0
        GIT_SHALLOW TRUE)
FetchContent_MakeAvailable(nanobench)

add_definitions(-DBASE_DIR="${PROJECT_SOURCE_DIR}")

aux_source_directory(${PROJECT_SOURCE_DIR}/tests TEST_FILES)

add_executable(unittest ${TEST_FILES})
target_link_libraries(unittest PRIVATE ${PROJECT_NAME} doctest_with_main nanobench)
target_include_directories(unittest PRIVATE ${PROJECT_SOURCE_DIR}/tests ${PROJECT_SOURCE_DIR}/include)
add_test(NAME ${PROJECT_NAME}-unittest COMMAND unittest)
