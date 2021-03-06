configure_file (${CMAKE_SOURCE_DIR}/src/config.vala.cmake ${CMAKE_BINARY_DIR}/src/config.vala)

find_package(Vala REQUIRED)
include(ValaVersion)
ensure_vala_version("0.26" MINIMUM)

include(ValaPrecompile)
vala_precompile(VALA_C ${CMAKE_PROJECT_NAME}
    ./elementarySystemMonitor.vala
    ./MainWindow.vala
    ./Widgets/ProcessView.vala
    ./Widgets/Search.vala
    ./Widgets/Statusbar.vala
    ./Models/ApplicationProcessModel.vala
    ./Managers/AppManager.vala
    ./Managers/ProcessManager.vala
    ./Managers/Process.vala
    ./Services/Settings.vala
    ./Services/Shortcuts.vala
    ./Services/Resources.vala
    ${CMAKE_BINARY_DIR}/src/config.vala
PACKAGES
    ${SYSTEM_MONITOR_DEPS}
    posix
CUSTOM_VAPIS
    ../vapi/libgtop-2.0.vapi
OPTIONS
    # --vapidir=${CMAKE_SOURCE_DIR}/vapi/
    --thread
    --enable-checking
    --enable-experimental
    -v
    -g
)

add_executable(${EXEC_NAME} ${VALA_C})
# install the binaries we just made
install (TARGETS ${EXEC_NAME} RUNTIME DESTINATION bin)
