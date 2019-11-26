add_executable(HelloWorld "${CMAKE_CURRENT_SOURCE_DIR}/HelloWorld.cpp")
target_compile_options(HelloWorld PRIVATE ${MAIN_CXX_FLAGS})
target_link_libraries(HelloWorld Box2D)
target_include_directories(HelloWorld PUBLIC
  "${CMAKE_CURRENT_SOURCE_DIR}/../Box2D"
)
