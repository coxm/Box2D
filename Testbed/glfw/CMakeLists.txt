set(GLFW_SOURCES
  "${CMAKE_CURRENT_SOURCE_DIR}/context.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/init.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/input.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/monitor.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/vulkan.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/window.c")
if(WIN32)
  set(GLFW_SOURCES ${GLFW_SOURCES}
    "${CMAKE_CURRENT_SOURCE_DIR}/glfw_config.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/glfw3.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/glfw3native.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/init.c")
elseif(APPLE)
  set(GLFW_SOURCES ${GLFW_SOURCES}
    "${CMAKE_CURRENT_SOURCE_DIR}/cocoa_platform.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/iokit_joystick.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/posix_tls.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/nsgl_context.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/egl_context.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/cocoa_init.m"
    "${CMAKE_CURRENT_SOURCE_DIR}/cocoa_joystick.m"
    "${CMAKE_CURRENT_SOURCE_DIR}/cocoa_monitor.m"
    "${CMAKE_CURRENT_SOURCE_DIR}/cocoa_window.m"
    "${CMAKE_CURRENT_SOURCE_DIR}/cocoa_time.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/posix_tls.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/nsgl_context.m"
    "${CMAKE_CURRENT_SOURCE_DIR}/egl_context.c")
else()
  set(GLFW_SOURCES ${GLFW_SOURCES}
    "${CMAKE_CURRENT_SOURCE_DIR}/xkb_unicode.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/linux_joystick.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/posix_time.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/posix_tls.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/glx_context.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/egl_context.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/x11_init.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/x11_monitor.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/x11_window.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/glx_context.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/glx_context.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/glext.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/xkb_unicode.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/linux_joystick.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/posix_time.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/posix_tls.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/glx_context.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/egl_context.c")
endif()
add_library(glfw ${GLFW_SOURCES})
set_target_properties(glfw PROPERTIES LINKER_LANGUAGE CXX)
target_include_directories(glfw PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
