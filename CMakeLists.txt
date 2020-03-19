project(Bro-Plugin-FOO)

cmake_minimum_required(VERSION 2.8)

include(BroPlugin)

bro_plugin_begin(Foo FOO)
bro_plugin_cc(src/Plugin.cc)
bro_plugin_cc(src/FOO.cc)
bro_plugin_bif(src/foo.bif)
bro_plugin_pac(src/foo.pac)
bro_plugin_dist_files(README COPYING VERSION)
bro_plugin_end()

file(STRINGS "${CMAKE_CURRENT_SOURCE_DIR}/VERSION" VERSION LIMIT_COUNT 1)

if ("${PROJECT_SOURCE_DIR}" STREQUAL "${CMAKE_SOURCE_DIR}")
    # Allows building rpm/deb packages via "make package" in build dir.
    include(ConfigurePackaging)
    ConfigurePackaging(${VERSION})
endif ()
