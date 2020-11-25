
option(RCJSIM_USE_SYSTEM_BULLET "Use system-wide install of Bullet instead of building it yourself." OFF)
IF(${RCJSIM_USE_SYSTEM_BULLET})
	message("Using system Bullet")

	find_package(Bullet 3.05 REQUIRED)

	# export library paths to parent scope
	set(BULLET_FOUND ${BULLET_FOUND} PARENT_SCOPE)
	set(BULLET_INCLUDE_DIRS ${BULLET_INCLUDE_DIRS} PARENT_SCOPE)
	set(BULLET_LIBRARIES ${BULLET_LIBRARIES} PARENT_SCOPE)
ELSE()
	message("Building own Bullet")

	# remove some unneeded features from the build targets
	set(BUILD_CPU_DEMOS OFF CACHE BOOL "Build Bullet CPU Demos")
	set(BUILD_PYBULLET OFF CACHE BOOL "Build PyBullet Python Interface")
	set(BUILD_ENET OFF CACHE BOOL "Build Bullet ENET support")
	set(BUILD_CLSOCKET OFF CACHE BOOL "Build Bullet ENET support")
	set(BUILD_EGL OFF CACHE BOOL "Build Bullet EGL")
	set(BUILD_BULLET3 OFF CACHE BOOL "Build Bullet3")
	set(BUILD_OPENGL3_DEMOS OFF CACHE BOOL "Build Bullet3 demos")
	set(BUILD_BULLET2_DEMOS OFF CACHE BOOL "Build Bullet2 demos")
	set(BUILD_EXTRAS OFF CACHE BOOL "Build Bullet extras")
	set(BUILD_UNIT_TESTS OFF CACHE BOOL "Build Bullet unit tests")

	add_subdirectory(bullet3)

	# export library paths to parent scope
	set(BULLET_FOUND TRUE PARENT_SCOPE)
	set(BULLET_INCLUDE_DIRS "${CMAKE_CURRENT_LIST_DIR}/bullet3/src" PARENT_SCOPE)
	set(BULLET_LIBRARIES "BulletInverseDynamics;BulletDynamics;BulletSoftBody;BulletCollision;LinearMath" PARENT_SCOPE)
ENDIF()

option(RCJSIM_USE_SYSTEM_OSG "Use system-wide install of OpenSceneGraph instead of building it yourself." OFF)
IF(${RCJSIM_USE_SYSTEM_OSG})
	message("Using system OSG")

	# find osg
	find_package(OpenSceneGraph 3.6 REQUIRED)
	find_package(osgViewer 3.6 REQUIRED)
	find_package(osgGA 3.6 REQUIRED)

	# export library paths to parent scope
	set(OPENSCENEGRAPH_FOUND ${OPENSCENEGRAPH_FOUND} PARENT_SCOPE)
	set(OPENSCENEGRAPH_INCLUDE_DIRS ${OPENSCENEGRAPH_INCLUDE_DIRS} PARENT_SCOPE)
	set(OPENSCENEGRAPH_LIBRARIES ${OPENSCENEGRAPH_LIBRARIES} PARENT_SCOPE)
	set(OSGVIEWER_LIBRARY ${OSGVIEWER_LIBRARY} PARENT_SCOPE)
	set(OSGGA_LIBRARY ${OSGGA_LIBRARY} PARENT_SCOPE)
ELSE()
	message("Building own OSG")

	# use bleeding edge technology from 2008
	set(OPENGL_PROFILE "GLCORE" CACHE STRING "OpenSceneGraph OpenGL profile")

	# disable unneeded features
	set(OSG_USE_DEPRECATED_API OFF CACHE BOOL "Build OpenSceneGraph deprecated API")
	set(BUILD_OSG_APPLICATIONS OFF CACHE BOOL "Build OpenSceneGraph applications")
	set(BUILD_OSG_PLUGINS_BY_DEFAULT OFF CACHE BOOL "Build all OpenSceneGraph plugins")
	# but force some plugins for model loading
	set(BUILD_OSG_PLUGIN_OBJ ON)
	set(BUILD_OSG_PLUGIN_STL ON)
	set(BUILD_OSG_PLUGIN_PNG ON)
	set(BUILD_OSG_PLUGIN_JPEG ON)

	add_subdirectory(osg)
	# if someone knows how to get osg to link with opengl correctly, tell me:
	find_package(OpenGL 3.1 REQUIRED)
	target_link_libraries(osg ${OPENGL_LIBRARIES})

	# export library paths to parent scope
	set(OPENSCENEGRAPH_FOUND TRUE PARENT_SCOPE)
	set(OPENSCENEGRAPH_INCLUDE_DIRS "${CMAKE_CURRENT_LIST_DIR}/osg/include;${CMAKE_CURRENT_BINARY_DIR}/osg/include" PARENT_SCOPE)
	set(OPENSCENEGRAPH_LIBRARIES "osg;OpenThreads" PARENT_SCOPE)
	set(OSGVIEWER_LIBRARY "osgViewer" PARENT_SCOPE)
	set(OSGGA_LIBRARY "osgGA" PARENT_SCOPE)
ENDIF()

