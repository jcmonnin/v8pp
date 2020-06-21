cmake_minimum_required(VERSION 3.13)

project(Test)


set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


add_library(v8pp
  v8pp/call_from_v8.hpp
  v8pp/call_v8.hpp
  v8pp/class.hpp
  v8pp/config.hpp
  v8pp/context.hpp
  v8pp/convert.hpp
  v8pp/function.hpp
  v8pp/json.hpp
  v8pp/module.hpp
  v8pp/object.hpp
  v8pp/property.hpp
  v8pp/ptr_traits.hpp
  v8pp/throw_ex.hpp
  v8pp/utility.hpp
  v8pp/version.hpp

  v8pp/class.ipp
  v8pp/json.ipp
  v8pp/throw_ex.ipp
  v8pp/version.ipp

  v8pp/class.cpp
  v8pp/context.cpp
  v8pp/convert.cpp
  v8pp/json.cpp
  v8pp/throw_ex.cpp
  v8pp/version.cpp
)

target_include_directories(v8pp PUBLIC . "packages/v8-v142-x64.8.0.426.28/include")
target_compile_definitions(v8pp PUBLIC V8_COMPRESS_POINTERS V8_31BIT_SMIS_ON_64BIT_ARCH)
# linking to v8 omitted because wanting to debug compile issue


add_executable(v8ppTest
  test/console.js
  test/file.js
  test/main.cpp
  test/test.hpp
  test/test_call_from_v8.cpp
  test/test_call_v8.cpp
  test/test_class.cpp
  test/test_context.cpp
  test/test_convert.cpp
  test/test_function.cpp
  test/test_json.cpp
  test/test_module.cpp
  test/test_object.cpp
  test/test_property.cpp
  test/test_ptr_traits.cpp
  test/test_throw_ex.cpp
  test/test_utility.cpp
)

target_link_libraries(v8ppTest v8pp)