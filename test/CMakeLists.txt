Include(FetchContent)

FetchContent_Declare(
  Catch2
  GIT_REPOSITORY https://github.com/catchorg/Catch2.git
  GIT_TAG        v2.13.1)

FetchContent_MakeAvailable(Catch2)

set(target_name eventcpp_test)

add_executable(${target_name} test.cpp
                              notify_with_params.cpp
                              notify_multiple.cpp)
target_link_libraries(${target_name} PUBLIC eventcpp)
target_link_libraries(${target_name} PRIVATE Catch2::Catch2)
target_include_directories(${target_name} PUBLIC ${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})

list(APPEND CMAKE_MODULE_PATH ${catch2_SOURCE_DIR}/contrib)
include(CTest)
include(ParseAndAddCatchTests)
ParseAndAddCatchTests(${target_name})