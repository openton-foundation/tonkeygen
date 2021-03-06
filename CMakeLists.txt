# This file is part of TON Key Generator,
# a desktop application for the TON Blockchain project.
#
# For license and copyright information please follow this link:
# https://github.com/ton-blockchain/tonkeygen/blob/master/LEGAL

cmake_minimum_required(VERSION 3.16)
cmake_policy(SET CMP0076 NEW)
cmake_policy(SET CMP0091 NEW)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

include(cmake/validate_special_target.cmake)
include(cmake/version.cmake)
desktop_app_parse_version(Keygen/build/version)

project(Keygen
    LANGUAGES C CXX
    VERSION ${desktop_app_version_cmake}
    DESCRIPTION "TON Key Generator"
    HOMEPAGE_URL "https://generator.ton.org"
)
set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT Keygen)

get_filename_component(third_party_loc "Keygen/ThirdParty" REALPATH)
get_filename_component(submodules_loc "Keygen" REALPATH)

include(cmake/variables.cmake)
include(cmake/nice_target_sources.cmake)
include(cmake/target_link_static_libraries.cmake)
include(cmake/target_link_frameworks.cmake)
include(cmake/init_target.cmake)
include(cmake/generate_target.cmake)

include(cmake/options.cmake)

include(cmake/external/qt/package.cmake)

set(desktop_app_skip_libs
    dbusmenu_qt
    ffmpeg
    hunspell
    iconv
    lz4
    minizip
    openal
    opus
    qr_code_generator
    sp_media_key_tap
    statusnotifieritem
)
set(DESKTOP_APP_LOTTIE_USE_CACHE OFF)

add_subdirectory(cmake)
add_subdirectory(Keygen)
