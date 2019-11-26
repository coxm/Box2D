# CMakeLists.txt for Box2D library, Testbed and HelloWorld application.
# Based on an article by Pablo Arias:
# https://pabloariasal.github.io/2018/02/19/its-time-to-do-cmake-right/
cmake_minimum_required(VERSION 3.7)
project(Box2D VERSION 2.3.1 LANGUAGES CXX)

include(CMakePackageConfigHelpers)
include(GNUInstallDirs)

option(BOX2D_BUILD_HELLO_WORLD "Build Box2D HelloWorld demo" OFF)
option(BOX2D_BUILD_TESTBED "Build the Box2D Testbed" OFF)


# Define Box2D library.
add_library(Box2D
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Common/b2Timer.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Common/b2Draw.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Common/b2Settings.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Common/b2Math.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Common/b2BlockAllocator.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Common/b2StackAllocator.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/b2BroadPhase.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/b2Collision.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/Shapes/b2EdgeShape.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/Shapes/b2ChainShape.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/Shapes/b2CircleShape.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/Shapes/b2PolygonShape.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/b2CollideCircle.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/b2Distance.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/b2CollidePolygon.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/b2DynamicTree.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/b2TimeOfImpact.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Collision/b2CollideEdge.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/b2WorldCallbacks.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2DistanceJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2PrismaticJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2RopeJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2MotorJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2FrictionJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2Joint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2WheelJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2RevoluteJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2GearJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2MouseJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2PulleyJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Joints/b2WeldJoint.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/b2World.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/b2ContactManager.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/b2Island.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/b2Fixture.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Contacts/b2PolygonContact.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Contacts/b2PolygonAndCircleContact.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Contacts/b2ContactSolver.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Contacts/b2ChainAndPolygonContact.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Contacts/b2EdgeAndCircleContact.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Contacts/b2CircleContact.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Contacts/b2EdgeAndPolygonContact.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Contacts/b2ChainAndCircleContact.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/Contacts/b2Contact.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Dynamics/b2Body.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/Box2D/Rope/b2Rope.cpp"
)
add_library(Box2D::Box2D ALIAS Box2D)
set_target_properties(Box2D PROPERTIES
  VERSION "${PROJECT_VERSION}"
  SOVERSION "${PROJECT_VERSION}"
  PROJECT_LABEL "Box2D"
  DEBUG_POSTFIX d
)

target_include_directories(Box2D
  PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)
target_compile_options(Box2D PRIVATE $<$<CXX_COMPILER_ID:GNU>:-Wall>)


configure_package_config_file(
  "${PROJECT_SOURCE_DIR}/Box2DConfig.cmake.in"
  "${PROJECT_BINARY_DIR}/Box2DConfig.cmake"
  INSTALL_DESTINATION "${CMAKE_INSTALL_DATADIR}/cmake/Box2D"
)
write_basic_package_version_file(
  "${PROJECT_BINARY_DIR}/Box2DConfigVersion.cmake"
  COMPATIBILITY AnyNewerVersion
)


configure_file(Box2D.pc.in Box2D.pc @ONLY)


# Install targets.
install(TARGETS Box2D
  EXPORT Box2D-targets
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})
install(DIRECTORY ${PROJECT_SOURCE_DIR}/Box2D
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
  FILES_MATCHING PATTERN "*.h")
install(EXPORT Box2D-targets
  FILE Box2DTargets.cmake
  NAMESPACE Box2D::
  DESTINATION "${CMAKE_INSTALL_DATADIR}/cmake/Box2D")
install(
  FILES
    "${PROJECT_BINARY_DIR}/Box2DConfig.cmake"
    "${PROJECT_BINARY_DIR}/Box2DConfigVersion.cmake"
  DESTINATION "${CMAKE_INSTALL_DATADIR}/cmake/Box2D")
install(
  FILES "${PROJECT_BINARY_DIR}/Box2D.pc"
  DESTINATION "${CMAKE_INSTALL_DATADIR}/pkgconfig")
export(EXPORT Box2D-targets
  FILE "${CMAKE_CURRENT_BINARY_DIR}/Box2DTargets.cmake"
  NAMESPACE Box2D::)
export(PACKAGE Box2D)


if(BOX2D_BUILD_HELLO_WORLD)
  add_subdirectory(HelloWorld)
endif()
if(BOX2D_BUILD_TESTBED)
  add_subdirectory(Testbed)
endif()
