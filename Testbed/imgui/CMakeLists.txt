add_library(imgui
  "${CMAKE_CURRENT_SOURCE_DIR}/imgui.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/imgui_demo.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/imgui_draw.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/imgui_impl_glfw_gl3.cpp")
target_include_directories(imgui PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(imgui PUBLIC Box2D glad glfw)
