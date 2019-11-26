add_subdirectory(glad)
add_subdirectory(glfw)
add_subdirectory(imgui)
add_subdirectory(Framework)


# Testbed executable.
add_executable(Testbed "${CMAKE_CURRENT_SOURCE_DIR}/Tests/TestEntries.cpp")
target_link_libraries(Testbed PRIVATE
  Box2DTestbedFramework Box2D::Box2D imgui glfw glad)
if(WIN32)
  target_link_libraries(Testbed PRIVATE opengl32 winmm)
elseif(APPLE)
  message(WARNING "Required Apple config unknown (help welcome)")
elseif(UNIX)
  find_package(OpenGL REQUIRED)
  target_link_libraries(Testbed PRIVATE
    Box2DTestbedFramework
    Xinerama Xcursor Xrandr pthread X11 dl ${OPENGL_LIBRARIES})
endif()
