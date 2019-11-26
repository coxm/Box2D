add_library(Box2DTestbedFramework
  "${CMAKE_CURRENT_SOURCE_DIR}/DebugDraw.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Test.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Main.cpp")
target_include_directories(Box2DTestbedFramework PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(Box2DTestbedFramework PUBLIC
  Box2D imgui glad glfw ${OPENGL_LIBRARIES})
