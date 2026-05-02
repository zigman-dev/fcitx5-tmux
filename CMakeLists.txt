cmake_minimum_required(VERSION 3.13)

project(fcitx5-tmux)

include(FeatureSummary)
include(GNUInstallDirs)

find_package(Fcitx5Utils REQUIRED)

include("${FCITX_INSTALL_CMAKECONFIG_DIR}/Fcitx5Utils/Fcitx5CompilerSettings.cmake")

add_subdirectory(src)

configure_file(fcitx5.tmux.in fcitx5.tmux @ONLY)
install(PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/fcitx5.tmux DESTINATION ${CMAKE_INSTALL_DATADIR}/tmux-fcitx5)

set(CPACK_DEBIAN_PACKAGE_DEPENDS "dbus-bin, tmux, fcitx5, libc6 (>= 2.38), libfcitx5utils2 (>= 5.1.17), libgcc-s1 (>= 3.0), libstdc++6 (>= 13.1)")
set(CPACK_DEBIAN_PACKAGE_REPLACES "fcitx5-frontend-tmux")
set(CPACK_PACKAGE_CONTACT "zigman <zigman.hsu@gmail.com>")
include (CPack)
