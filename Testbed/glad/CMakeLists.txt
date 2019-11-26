add_library(glad
    "${CMAKE_CURRENT_SOURCE_DIR}/glad.c")
set_target_properties(glad PROPERTIES LINKER_LANGUAGE CXX)
target_include_directories(glad PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(glad glfw ${OPENGL_LIBRARIES})
